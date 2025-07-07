---
layout: home

hero:
  name: "buzzts"
  text: 常用的工具函数
  tagline: 共300个工具函数，帮助提高开发效率
  image:
    src: /buzzts.svg
    alt: "buzzts"
  actions:
    - theme: brand buzzts-start
      text: 快速开始
      link: /guide/guide
    - theme: alt buzzts-github
      text: 文档仓库
      link: https://github.com/kamalyes/buzzts-docs
      
features:
  - icon: ⚡️
    title: 短小精悍，代码轻量
    details: 适用于现代ES6/2020规范
  - icon: 💫
    title: 零依赖
    details: 零Dependencies依赖，只会安装项目本身
  - icon: 📡
    title: 可通过CDN引用
    details: 同时支持jsdelivr和unpkg
  - icon: 🦾
    title: 基于 TypeScript 开发
    details: 类型安全，强大的类型推导
  - icon: 🌎
    title: 动态插件库
    details: 随时调用，提供全面的工具库
  - icon: 🧪
    title: 测试覆盖
    details: 使用 Jest 进行了测试，确保代码质量
  - icon: 🔧
    title: 兼容性
    details: 兼容各种 JavaScript 环境
  - icon: 📐
    title: 场景覆盖
    details: 覆盖日常开发的大部分场景，从基础工具到高级功能，一应俱全
  - icon: 📦
    title: 打包工具
    details: 使用 Rollup 打包，优化性能
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
