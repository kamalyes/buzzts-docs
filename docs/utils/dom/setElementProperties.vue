<template>
  <div>
    <h2>设置CSS自定义属性</h2>
    <n-button type="primary" @click="setProperties">设置属性</n-button>
    <div id="target" style="width: 100px; height: 100px; background: var(--primary-color);"></div>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { setElementProperties, randColorHEX } from 'buzzts';

// 定义设置自定义属性的函数
const setProperties = () => {
  const target = document.documentElement; // 获取根元素
  setElementProperties(target, {
    '--primary-color': randColorHEX(), // 设置新颜色
  });
};

onMounted(()=>{
  setProperties();
})
</script>

<style>
/* 可以根据需要添加样式 */
</style>
