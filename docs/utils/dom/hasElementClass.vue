<template>
  <n-card vertical>
    <n-switch v-model="isHidden" @update:value="toggleClass">Toggle Hidden Class</n-switch>
    <div ref="element" :class="{ hidden: isHidden }">Hello World</div>
    <p>Class 'hidden' {{ classExists }}!</p>
  </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { hasElementClass } from 'buzzts';

// 定义响应式变量
const element = ref<HTMLElement | null>(null);
const classExists = ref(false);
const isHidden = ref(false); // 控制 hidden 类的状态

// 切换类的函数
const toggleClass = (value: boolean) => {
  if (element.value) {
    if (value) {
      element.value.classList.add('hidden');
    } else {
      element.value.classList.remove('hidden');
    }
  }
  checkClass();
};

// 检查类是否存在的函数
const checkClass = () => {
  if (element.value) {
    classExists.value = hasElementClass(element.value, 'hidden');
  }
};
</script>

<style>
.hidden {
  display: none; /* 隐藏元素 */
}
</style>
