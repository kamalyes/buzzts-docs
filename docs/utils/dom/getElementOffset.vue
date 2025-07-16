<template>
  <div>
    <h2>获取元素偏移量</h2>
    <n-button type="primary" @click="getOffset">获取偏移量</n-button>
    <pre>{{ offset }}</pre>
    <div id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementOffset } from 'buzzts';

const offset = ref<{ top: number; left: number } | null>(null);

const getOffset = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  offset.value = getElementOffset(element);
};
</script>
