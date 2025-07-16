<template>
  <div>
    <div ref="element" style="width: 100px; height: 100px; background: red;"></div>
    <n-button type="primary" @click="animate">Animate</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { animateTo } from 'buzzts';

// 使用 ref 创建对 DOM 元素的引用
const element = ref<HTMLElement | null>(null);

// 动画函数
const animate = () => {
  if (element.value) {
    animateTo(
      element.value,
      [
        { transform: 'scale(1)' },
        { transform: 'scale(1.5)' },
        { transform: 'scale(1)' }
      ],
      1000
    );
  }
};
</script>

<style scoped>
/* 添加一些样式（可选） */
</style>
Argument of type '{ duration: number; }' is not assignable to parameter of type 'number'.Vetur(2345)
