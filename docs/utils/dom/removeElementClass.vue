<template>
  <div>
    <div ref="element" class="active">Hello World</div>
    <n-button type="primary" @click="removeClass">Remove Class</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { removeElementClass } from 'buzzts';

// 定义响应式变量
const element = ref<HTMLElement | null>(null);

// 定义移除类的函数
const removeClass = () => {
  if (element.value) {
    removeElementClass(element.value, 'active');
  }
};
</script>

<style>
.active {
  color: blue;
}
</style>
