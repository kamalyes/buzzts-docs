<template>
  <div>
    <h2>Event Delegation Demo</h2>
    <div ref="parent" class="parent-container">
      <n-button class="child-n-button">按钮 1</n-button>
      <n-button class="child-n-button">按钮 2</n-button>
      <n-button class="child-n-button">按钮 3</n-button>
    </div>
    <p>点击上面的按钮以查看事件委托效果。</p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { delegateElementEvent } from 'buzzts';

const parent = ref<HTMLElement | null>(null); // 明确指定类型

const handlebuttonClick = (el: HTMLElement, event: Event) => {
  alert(`你点击了 ${el.textContent}`);
};

onMounted(() => {
  // 使用事件委托
  if (parent.value) {
    delegateElementEvent(parent.value, 'click', '.child-n-button', handlebuttonClick);
  }
});
</script>

<style scoped>
.parent-container {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}

.child-n-button {
  margin: 5px;
}
</style>
