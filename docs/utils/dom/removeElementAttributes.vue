<template>
  <div>
    <h2>移除元素属性</h2>
    <n-button type="primary" @click="removeAttributes">移除属性</n-button>
    <div id="myElement" class="new-class" data-custom="value">这是一个示例元素</div>
    <pre v-if="Object.keys(attributes).length > 0">{{ attributes }}</pre>
  </div>
</template>

<script setup lang="ts">
import { ref, nextTick, onMounted } from 'vue';
import { removeElementAttributes, getElementAttributes, setElementAttributes } from 'buzzts';

const attributes = ref<Record<string, string>>({});

// 定义 fetchAttributes 函数
const fetchAttributes = async () => {
  await nextTick(); // 等待 DOM 更新
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    attributes.value = getElementAttributes(myElement);
  }
};

const setAttributes = () => {
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    setElementAttributes(myElement, {
      'data-custom': "1235678",
      'class': "ima"
    });
  }
  fetchAttributes();
};

const removeAttributes = () => {
  const myElement = document.getElementById('myElement') as HTMLElement;
  if (myElement) {
    removeElementAttributes(myElement, ['data-custom', 'class']);
  }
  fetchAttributes();
};

onMounted(()=>{
  setAttributes();
  fetchAttributes();
})
</script>
