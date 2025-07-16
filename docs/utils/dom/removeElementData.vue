<template>
  <div>
    <div ref="element" data-user-id="123">Hello World</div>
    <n-button type="primary" @click="removeData">Remove Data Attribute</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { removeElementData } from 'buzzts'; // 确保导入你的函数

// 定义响应式变量
const element = ref<HTMLElement | null>(null);

// 定义移除数据属性的函数
const removeData = () => {
  if (element.value) {
    removeElementData(element.value, 'userId');
    element.value.textContent = `Data-userId: Removed`;
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
