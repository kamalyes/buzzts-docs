<script setup lang="ts">
import { ref, computed } from "vue";
import { isBoolean } from "buzzts";

const val = ref<any>(true);
const result = ref<boolean | null>(null);

function checkIsBoolean() {
  result.value = isBoolean(val.value);
}

const resultText = computed(() => {
  if (result.value === null) return "请输入值后点击检测是否为布尔值";
  return `isBoolean(${JSON.stringify(val.value)}) = ${result.value}`;
});
</script>

<template>
  <n-card title="判断是否为布尔值">
    <n-space vertical>
      <n-input v-model:value="val" placeholder="请输入任意值" clearable />
      <n-button type="primary" @click="checkIsBoolean">检测</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
