<template>
  <n-card title="设置元素属性">
    <n-space vertical >
      <div id="myElement">这是一个示例元素</div>
      <n-button type="primary" @click="setAttributes">设置附加属性</n-button>
      <pre v-if="Object.keys(attributes).length > 0">{{ attributes }}</pre>
    </n-space>
  </n-card>
</template>

<script setup lang="ts">
import { ref, nextTick, onMounted } from 'vue';

import { setElementAttributes, getElementAttributes, randString, RandType } from 'buzzts';
const attributes = ref<Record<string, string>>({});

// 定义 fetchAttributes 函数
const fetchAttributes = async () => {
  await nextTick(); // 等待 DOM 更新
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    attributes.value = getElementAttributes(myElement);
  }
};

const setAttributes = () => {
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    setElementAttributes(myElement, {
      'data-custom': randString(10, RandType.CAPITAL | RandType.NUMBER),
      'class': randString(10, RandType.CAPITAL | RandType.NUMBER)
    });
  }
  fetchAttributes();
};

onMounted(()=>{
  fetchAttributes();
})
</script>
