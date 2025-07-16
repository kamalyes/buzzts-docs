<template>
  <div>
    <h2>获取元素计算样式</h2>
    <n-button type="primary" @click="getStyle">获取样式</n-button>
    <div ref="target" :style="defaultAfterStyle"></div>
    <p v-if="computedStyle != null">计算后的样式: {{ computedStyle }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementStyle } from 'buzzts';
import { randInt } from 'buzzts';

// 定义响应式变量
const computedStyle = ref(null);
const target = ref<HTMLElement | null>(null); // 定义 target 的 ref
const defaultAfterStyle = ref(`width: 150px; height: 150px; background: lightblue; margin-top: ${randInt(10, 20)}px;`);

// 提取获取样式的逻辑到外部函数
const fetchElementStyles = (element: HTMLElement) => {
  return {
    width: getElementStyle(element, 'width'),
    height: getElementStyle(element, 'height'),
    backgroundColor: getElementStyle(element, 'background-color'),
    marginTop: getElementStyle(element, 'margin-top'),
  };
};

// 获取样式的函数
const getStyle = () => {
  if (target.value) { // 直接使用 target.value
    computedStyle.value = fetchElementStyles(target.value); // 使用提取的函数
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
