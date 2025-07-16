<template>
  <div>
    <h2>设置自定义数据属性</h2>
    <n-button type="primary" @click="setData">设置用户ID</n-button>
    <div id="target">{{ userId }}</div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { setElementData, getElementData, randInt } from 'buzzts';

// 定义一个普通变量来显示用户ID
const userId = ref('用户OldID: 123456');

// 定义设置自定义数据属性的函数
const setData = () => {
  const target = document.getElementById('target');
  if (target) {
    const newUserId = `用户NewID: ${randInt(100000, 2000000000)}`; // 新的用户ID
    setElementData(target, 'userId', newUserId); // 设置自定义数据属性
    userId.value = getElementData(target, 'userId');
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
