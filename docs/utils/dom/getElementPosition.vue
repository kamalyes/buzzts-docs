<template>
  <div>
    <h2>获取元素位置</h2>
    <n-button type="primary" @click="getPosition">获取位置</n-button>
    <pre>{{ position }}</pre>
    <div id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getElementPosition } from 'buzzts';

const position = ref<DOMRect | null>(null);

const getPosition = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  position.value = getElementPosition(element);
};
</script>
