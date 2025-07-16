<template>
  <div>
    <div ref="target" style="margin-top: 1000px;">Scroll Target</div>
    <n-button type="primary" @click="scrollToTarget">Scroll to Target</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { smoothScrollTo } from 'buzzts';

// 使用 ref 创建一个对 DOM 元素的引用
const target = ref<HTMLElement | null>(null);

// 定义滚动到目标的函数
const scrollToTarget = () => {
  if (target.value) {
    smoothScrollTo(target.value);
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
