<template>
  <div>
    <h2>Append Element Children Demo</h2>
    <n-button type="primary" @click="addChildren">添加子元素</n-button>
    <div ref="parent" class="parent-container">
      <!-- 子元素将被追加到这里 -->
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { appendElementChildren } from 'buzzts';

const parent = ref<HTMLElement | null>(null);

const addChildren = () => {
  const childrenToAdd: (string | Node | null | undefined)[] = [
    '文本节点 1',
    document.createElement('div'),
    '文本节点 2',
    document.createElement('span'),
    null,        // 自动跳过
    undefined    // 自动跳过
  ];

  // 创建一个新的 div 作为子元素
  const newDiv = document.createElement('div');
  newDiv.textContent = '这是一个动态添加的 div';
  
  // 将 newDiv 添加到 childrenToAdd 数组中
  childrenToAdd.push(newDiv); // 将 newDiv 添加到数组

  // 使用 appendElementChildren 函数将子元素追加到父元素
  appendElementChildren(parent.value, childrenToAdd);
};
</script>

<style scoped>
.parent-container {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}
</style>
