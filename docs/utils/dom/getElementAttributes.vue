<template>
  <div>
    <h2>获取元素属性</h2>
    <div id="myElement" data-user-id="123" data-role="admin" class="test-element">
      测试元素
    </div>
    <n-button type="primary" @click="fetchAttributes">获取属性</n-button>
    <pre v-if="Object.keys(attributes).length > 0">{{ attributes }}</pre>
  </div>
</template>

<script setup lang="ts">
import { ref, nextTick } from 'vue';
import { getElementAttributes } from 'buzzts';

const attributes = ref<Record<string, string>>({});

// 定义 fetchAttributes 函数
const fetchAttributes = async () => {
  await nextTick(); // 等待 DOM 更新
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    attributes.value = getElementAttributes(myElement);
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
