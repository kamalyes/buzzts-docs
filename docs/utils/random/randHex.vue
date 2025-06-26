<script setup lang="ts">
import { ref, computed } from 'vue';
import { randHex } from 'buzzts';

const bytesLen = ref(4);
const customBytes = ref<string | undefined>(undefined); // 可选自定义16进制字符集
const hexResult = ref<string>('');

function generateHex() {
  hexResult.value = randHex(bytesLen.value, customBytes.value);
}

const resultText = computed(() => {
  if (!hexResult.value) return '点击生成随机十六进制字符串';
  return `randHex(${bytesLen.value}) = ${hexResult.value}`;
});
</script>

<template>
  <n-card title="随机十六进制字符串生成" style="max-width: 400px;">
    <n-space vertical size="large">
      <n-input-number v-model:value="bytesLen" :min="1" :max="20" label="字节长度" />
      <n-input v-model:value="customBytes" placeholder="自定义16进制字符集（可选）" />
      <n-button type="primary" @click="generateHex">生成随机十六进制字符串</n-button>

      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
