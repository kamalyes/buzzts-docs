---
layout: home

hero:
  name: "buzzts"
  text: 常用的工具函数
  tagline: 共300个工具函数，帮助提高开发效率
  image:
    src: /logo.png
    alt: "buzzts"
  actions:
    - theme: brand buzzts-start
      text: 快速开始
      link: /guide/guide
    - theme: alt buzzts-github
      text: 文档仓库
      link: https://github.com/kamalyes/buzzts-docs

features:
  - icon: 🌎
    title: 任意 JavaScript 环境中运行
    details: 支持 Node.js、浏览器以及任意 JavaScript 框架
  - icon: 📡
    title: 可通过 CDN 引用
    details: 同时支持 jsdelivr 和 unpkg
  - icon: ⚡️
    title: 完全可摇树
    details: 自带 Tree-shaking ，只对引入的代码进行打包
  - icon: 💫
    title: 零依赖
    details: 零 Dependencies 依赖，只会安装项目本身
  - icon: 🦾
    title: 强类型
    details: 使用 TypeScript 编写，拥有强大的类型推导提示
  - icon: 💯
    title: 100%测试
    details: 100% 测试覆盖率，100% 测试通过率
---

<script setup>
  
import './.vitepress/theme/style/home-links.css'
import { onMounted } from 'vue'
// import { useMessage } from "./components/message"
import { addReleaseTag } from './.vitepress/utils/createElement.ts'

onMounted(() => {
  addReleaseTag()
})
</script>
