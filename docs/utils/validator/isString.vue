<script setup lang="ts">
import { ref, computed } from "vue";
import { isString } from "buzzts";

const val = ref<any>("abc");
const result = ref<boolean | null>(null);

function checkIsString() {
  result.value = isString(val.value);
}

const resultText = computed(() => {
  if (result.value === null) return "请输入值后点击检测是否为字符串";
  return `isString(${JSON.stringify(val.value)}) = ${result.value}`;
});
</script>

<template>
  <n-card title="判断是否为字符串">
    <n-space vertical>
      <n-input v-model:value="val" placeholder="请输入任意值" clearable />
      <n-button type="primary" @click="checkIsString">检测</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
