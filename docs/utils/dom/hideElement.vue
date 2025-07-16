<template>
  <div>
    <h2>隐藏元素</h2>
    <n-button type="primary" @click="hide">隐藏元素</n-button>
    <div :hidden="hiddenMyElement" id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { hideElement, getElementStyle } from 'buzzts';

const hiddenMyElement = ref(false)

const hide = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  hideElement(element);
  // 获取元素的 display 属性
  const displayValue = getElementStyle(element, "display");
  // 根据 display 属性的值更新 hiddenMyElement
  hiddenMyElement.value = displayValue === 'none';
};
</script>
