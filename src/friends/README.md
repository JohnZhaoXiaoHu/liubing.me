---
toc: false
pageInfo: false
panelRenderTag: 'a'
---

# 友情链接

```
站点名称：Bing🐣
站点地址：https://liubing.me
站点描述：基于VuePress的个人博客，记录日常开发问题。
站点Logo：https://liubing.me/logo.png
```

请先将本站加入友链后，在下方评论按如下格式提供信息：

```
icon: '网站图标'
name: '网站名字'
desc: '网站描述'
link: '网站链接'
```

## 固定链接

<ProjectPanel :projects="projects1" />

## 友链链接

<ProjectPanel :projects="projects2" />

<script setup lang="ts">
  const projects1 = [
    {
      icon: 'https://cn.vuejs.org/logo.svg',
      name: 'Vue',
      desc: '渐进式 JavaScript 框架',
      link: 'https://cn.vuejs.org/'
    },
    {
      icon: 'https://v2.vuepress.vuejs.org/images/hero.png',
      name: 'VuePress',
      desc: 'Vue 驱动的静态网站生成器',
      link: 'https://v2.vuepress.vuejs.org/zh/'
    },
    {
      icon: 'https://theme-hope.vuejs.press/logo.png',
      name: 'VuePress Theme Hope',
      desc: '一个具有强大功能的 vuepress 主题✨',
      link: 'https://theme-hope.vuejs.press/zh/'
    },
    {
      icon: 'https://image.liubing.me/2022/12/30/c827badf9fa7a.jpg',
      name: 'iconfont',
      desc: '阿里巴巴矢量图标库。',
      link: 'https://www.iconfont.cn/'
    }
  ]
  const projects2 =  [
    {
      icon: 'https://file.mo7.cc/static/lxh_gif/lxh_71.gif',
      name: '墨七',
      desc: '简单快乐，理应如此。',
      link: 'https://blog.mo7.cc/'
    },
    {
      icon: 'https://blog.xxwhite.com/assets/img/avatar.jpg',
      name: '叉叉白',
      desc: 'MonoLogueChi',
      link: 'https://blog.xxwhite.com/'
    }
  ]
</script>
