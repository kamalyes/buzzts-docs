<template>
  <div>
    <h2>切换类名</h2>
    <n-button type="primary" @click="toggleClass">切换类名</n-button>
    <div ref="target" class="boxx"></div>
  </div>
</template>

<script setup lang="ts">
import { toggleElementClass } from 'buzzts';
import { ref } from 'vue';

// 使用 ref 创建对目标元素的引用
const target = ref<HTMLElement | null>(null);

// 定义一个方法来切换类名
const toggleClass = () => {
  if (target.value) {
    toggleElementClass(target.value, 'activexx');
  }
};
</script>

<style>
.boxx {
  width: 100px;
  height: 100px;
  background-color: lightgray;
  transition: background-color 0.3s; /* 添加过渡效果 */
}

.activexx {
  background-color: orange;
}
</style>
