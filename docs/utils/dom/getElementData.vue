<template>
  <div>
    <h2>获取自定义数据属性</h2>
    <n-button type="primary" @click="getData">获取数据属性</n-button>
    <div ref="target" data-user-id="12345">用户信息</div>
    <p>用户ID: {{ userId }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementData } from 'buzzts'; // 引入工具集

// 定义响应式变量
const userId = ref('');
const target = ref<HTMLElement | null>(null);

// 获取数据属性的函数
const getData = () => {
  if (target.value) {
    userId.value = getElementData(target.value, 'userId');
  }
};
</script>

<style scoped>
/* 可以根据需要添加样式 */
</style>
