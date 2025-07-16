<template>
  <div>
    <h2>获取元素位置信息</h2>
    <div ref="targetElement" class="target-element">
      想知道我的位置信息，点击【获取位置信息】
    </div>
    <n-button type="primary" @click="getRect">获取位置信息</n-button>
    <div v-if="rectInfo" class="rect-info">
      <p>宽度: {{ rectInfo.width }}px</p>
      <p>高度: {{ rectInfo.height }}px</p>
      <p>左边距: {{ rectInfo.left }}px</p>
      <p>上边距: {{ rectInfo.top }}px</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementRect } from 'buzzts';

// 引用目标元素和位置信息
const targetElement = ref<HTMLElement | null>(null);
const rectInfo = ref<{ width: number; height: number; left: number; top: number } | null>(null);

// 获取位置信息的函数
const getRect = () => {
  if (targetElement.value) {
    const rect = getElementRect(targetElement.value);
    rectInfo.value = {
      width: rect.width,
      height: rect.height,
      left: rect.left,
      top: rect.top,
    };
  }
};
</script>

<style scoped>
.target-element {
  border: 1px solid #007bff;
  padding: 20px;
  margin: 20px 0;
  text-align: center;
  cursor: pointer;
}

.rect-info {
  margin-top: 20px;
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
