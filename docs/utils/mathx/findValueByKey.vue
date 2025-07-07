<script setup lang="ts">
import { ref, computed } from 'vue';
import { findValueByKey } from 'buzzts';

// 设置默认值
const inputArray = ref<string>(JSON.stringify([{ id: '1', name: 'One' }, { id: '2', name: 'Two' }])); // 默认的 JSON 字符串
const searchKey = ref<string>('id'); // 默认查找键
const searchValue = ref<any>('1'); // 默认查找值
const returnKey = ref<any>(null);
const foundValue = ref<any>(null);

const findValue = () => {
  const parsedItems = JSON.parse(inputArray.value);
  if (returnKey.value === "") {
    returnKey.value = null;
  }
  foundValue.value = findValueByKey(parsedItems, searchKey.value, searchValue.value, returnKey.value);
};

const resultText = computed(() => {
  if (foundValue.value === null) return "未找到匹配的值";
  return `findValueByKey(${inputArray.value}, ${searchKey.value}, ${searchValue.value}, ${returnKey.value})= ${JSON.stringify(foundValue.value)}`;
});

</script>

<template>
  <n-card title="findValueByKey 示例">
    <n-space vertical>
      <div class="input-container">
        <n-input
          type="textarea"
          v-model:value="inputArray"
          placeholder="输入对象数组 (JSON 格式，例如: [{ id: '1', name: 'One' }, { id: '2', name: 'Two' }])"
          :rows="3"
        />
        <n-input
          v-model:value="searchKey"
          placeholder="要查找的键"
        />
        <n-input
          v-model:value="searchValue"
          placeholder="要查找的值"
        />
        <n-input
          v-model:value="returnKey"
          placeholder="返回的字段值"
        />
      </div>
      <n-button type="primary" @click="findValue">查找值</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>

<style scoped>
textarea {
  width: 100%;
  height: 100px;
}
.input-container {
  display: flex;
  flex-direction: column;
  gap: 10px; /* 控制输入框之间的间距 */
}
</style>
