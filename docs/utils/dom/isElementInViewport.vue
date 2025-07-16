<template>
  <div>
    <div ref="element" style="height: 200px; background: lightblue;">Scroll to see me!</div>
    <n-button type="primary" @click="checkVisibility">Check Visibility</n-button>
    <p v-if="isVisible">Element is in viewport!</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { isElementInViewport } from 'buzzts';

// 定义响应式变量
const element = ref<HTMLElement | null>(null);
const isVisible = ref(false);

// 检查元素是否在视口内的函数
const checkVisibility = () => {
  if (element.value) {
    isVisible.value = isElementInViewport(element.value, 0.5);
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
