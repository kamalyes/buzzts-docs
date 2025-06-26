<script setup lang="ts">
import { ref, computed } from 'vue';
import { randNumber } from 'buzzts';

const length = ref(6);
const customBytes = ref<string | undefined>(undefined); // 可选自定义数字字符集
const numberResult = ref<string>('');

function generateNumber() {
  numberResult.value = randNumber(length.value, customBytes.value);
}

const resultText = computed(() => {
  if (!numberResult.value) return '点击生成随机数字字符串';
  return `randNumber(${length.value}) = ${numberResult.value}`;
});
</script>

<template>
  <n-card title="随机数字字符串生成" style="max-width: 400px;">
    <n-space vertical size="large">
      <n-input-number v-model:value="length" :min="1" :max="20" label="长度" />
      <n-input v-model:value="customBytes" placeholder="自定义数字字符集（可选）" />
      <n-button type="primary" @click="generateNumber">生成随机数字字符串</n-button>

      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
