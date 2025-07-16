<template>
  <div>
    <h2>显示元素</h2>
    <n-button type="primary" @click="show">显示元素</n-button>
    <div :hidden="!visibleMyElement" id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { showElement, getElementStyle } from 'buzzts'; // 假设你有这个函数

const visibleMyElement = ref(false);

const show = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  showElement(element);
  // 获取元素的 display 属性
  const displayValue = getElementStyle(element, "display");
  // 根据 display 属性的值更新 visibleMyElement
  visibleMyElement.value = displayValue !== 'none';
};
</script>
