<template>
  <div>
    <div ref="element">Hello World</div>
    <n-button type="primary" @click="addClass">Add ElementClass</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { addElementClass } from 'buzzts';

// 使用 ref 创建对 DOM 元素的引用
const element = ref<HTMLElement | null>(null);

// 添加类的函数
const addClass = () => {
  if (element.value) {
    addElementClass(element.value, 'active');
  }
};
</script>

<style scoped>
.active {
  color: blue; /* 示例样式，您可以根据需要自定义 */
  font-weight: bold;
}
</style>
