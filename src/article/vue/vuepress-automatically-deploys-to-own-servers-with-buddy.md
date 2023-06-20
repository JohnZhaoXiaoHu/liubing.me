---
date: 2023-01-02
category:
  - Vue
  - VuePress
  - Buddy
tag:
  - Vue
  - 自动打包
  - 自动部署
  - 自动构建
layout: ArticleLayout
containerClass: article-container
---

# VuePress 借助 Buddy 自动构建打包部署到自己的服务器

近期将自己的博客由 `WordPress` 迁移到了 `VuePress`，一开始想到的是用 Github 提供的 Action 功能，代码推送到 main 分支后自动构建打包并将打包后的文件通过 FTP 的形式发送到自己的服务器上面，尴尬的是之前利用 Action 做了些非法用途，用于各种脚本签到导致 Action 功能被封了 😂，最后这个方法被弃用了，然后就找到了今天的主角：Buddy，记录下自动构建打包配置过程。

<!-- more -->

## 注册

::: tip
如果打不开 Buddy 官网，请开启魔法上网。
:::

没注册过的同学可以自行去 Buddy 官网注册：[点击前往](https://buddy.works)，推荐大家使用 GitHub 方式进行登录。

## 配置

注册登录完毕后自动进去控制台，点击控制台右上角的 `New project` 按钮新建项目。

![image](https://image.liubing.me/2023/01/02/12eaed79b6b9f.png)

选择仓库提供者为 Github，下面会列出自己的仓库列表，如果仓库列表出不来的话点击 `Can't see your repositories?`进行授权，选择一个仓库进入下一步。

![image](https://image.liubing.me/2023/01/02/6fb9e53a38638.png)

## 添加管道

点击右上角的 `New pipeline` 按钮新增一个管道。

![image](https://image.liubing.me/2023/01/02/aff9cc1dc453f.png)

选择配置类型为 `New`，填写 `Name` 名称，自己定义即可，选择触发类型为 `On events`，选择一个自己的分支。

![image](https://image.liubing.me/2023/01/02/9cfe376fe9aa7.png)

选择技术栈为 Node.js

![image](https://image.liubing.me/2023/01/02/8ceeca0aa31b4.png)

填写 VuePress 打包打包命令，可以使用 `npm` 或者 `yarn`，按需使用，考虑都打包后文件过多，如果单个单个发送的话耗时可能比较多，这里将打包的好的 `dist` 打成压缩包，完成后点击 `Add this action` 按钮添加步骤。

```sh
yarn install
yarn docs:build
cd src/.vuepress
tar -zcvf dist.tar.gz dist
```

![image](https://image.liubing.me/2023/01/02/1463771ba9845.png)

## 添加 FTP 配置

以上就配置好了打包的步骤，打完包后需要将打包好的文件通过 FTP 的形式发送到自己的服务器上。点击下方的 `+` 号添加其他步骤。

![ced3e027f638e](https://image.liubing.me/2023/01/02/ced3e027f638e.png)

可以通过搜索输入框输入 `FTP` 找到我们想要的服务，选择 `FTP`。

![d6da4a5fdbea5](https://image.liubing.me/2023/01/02/d6da4a5fdbea5.png)

![0982bce304cc5](https://image.liubing.me/2023/01/02/0982bce304cc5.png)

配置需要发送的源文件，这里选择 Pipeline Filesystem，填写源文件路径：

```
/src/.vuepress/dist.tar.gz
```

![image](https://image.liubing.me/2023/01/02/427048aebfdc2.png)

点击 Target 进行 FTP 相关的配置，此时需要填写一些 FTP 的配置信息，包括 FTP 地址、端口号、用户名、密码、路径信息。

![image](https://image.liubing.me/2023/01/02/9a317774277b6.png)

由于这些信息里面有敏感信息，可以在选择左侧的 `Variables, Keys & Assets` 菜单进行一些变量的配置。

![image](https://image.liubing.me/2023/01/02/bc4f320bdf561.png)

![image](https://image.liubing.me/2023/01/02/15f45c594b7b0.png)

变量配置完成后可以通过输入框右侧的$符号的按钮进行变量的选择。

![image](https://image.liubing.me/2023/01/02/42bf030f39504.png)

配置完成后可以点击下方的测试按钮进行测试联通性，联通性 OK 的话 `PATH` 选择可以点击右侧的按钮进行选择。这个`PATH`就是打包后的文件发送到服务器的位置。

::: warning
填写的 PATH 是个相对路径，比如你配置的 FTP 用户所在的目录是`/www/wwwroot/`，那么这里填写的 PATH 就是相对这个目录，如图上填写的`/vuepress`，对应的服务器目录就是`/www/wwwroot/vuepress`。
:::

![image](https://image.liubing.me/2023/01/02/a08fff8e90312.png)

## 添加 SSH 配置

打包后的压缩文件发送到服务器的具体位置后还需要进行解压操作，用同样的方法添加 SSH 步骤，填入相关配置。

```sh
# 进入到 vuepress 的目录，执行解压命令，完成后删除压缩包。
cd /www/wwwroot/liubing.me/vuepress
tar -zxvf dist.tar.gz
rm -rf dist.tar.gz
```

![image](https://image.liubing.me/2023/01/02/d25b2251377e6.png)

![image](https://image.liubing.me/2023/01/02/c60dfbe00771d.png)

## 测试打包

全部配置完成后就可以点击 Run 按钮执行管道任务，如果有出现红色的的提示，可以点击 `Logs` 按钮查看相关的日志信息排查问题。

![image](https://image.liubing.me/2023/01/02/e61da9a90204c.png)

![image](https://image.liubing.me/2023/01/02/673eaf93d0546.png)
