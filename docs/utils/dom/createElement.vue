<template>
  <div>
    <div ref="parent"></div>
    <n-button type="primary" @click="createNewElement">Create Element</n-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { createElement } from 'buzzts';

// 使用 ref 创建对父元素的引用
const parent = ref<HTMLElement | null>(null);

// 创建新元素的函数
const createNewElement = () => {
  if (parent.value) {
    const newElement = createElement('div', { class: 'new-element' }, 'I am a new element!');
    parent.value.appendChild(newElement);
  }
};
</script>

<style scoped>
.new-element {
  margin: 10px 0;
  padding: 10px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
