<template>
  <div>
    <h2>检查元素可见性</h2>
    <n-button type="primary" @click="checkVisibility">检查可见性</n-button>
    <pre>{{ visible }}</pre>
    <div id="myElement" style="margin-top: 20px; border: 1px solid #000; padding: 10px;">
      目标元素
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { isElementVisible } from 'buzzts';

const visible = ref<boolean>(false);

const checkVisibility = () => {
  const element = document.getElementById('myElement') as HTMLElement;
  visible.value = isElementVisible(element);
};
</script>
