<template>
  <div>
    <h2>获取元素大小</h2>
    <n-button type="primary" @click="getSize">获取大小</n-button>
    <pre>{{ size }}</pre>
    <div id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementSize } from 'buzzts';

const size = ref<{ width: number; height: number } | null>(null);

const getSize = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  size.value = getElementSize(element);
};
</script>
