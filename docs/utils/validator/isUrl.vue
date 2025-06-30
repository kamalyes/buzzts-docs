<script setup lang="ts">
import { ref, computed } from "vue";
import { isUrl } from "buzzts";

const val = ref<string>("https://www.example.com"); // 默认URL
const result = ref<boolean | null>(null);

function checkIsUrl() {
  result.value = isUrl(val.value);
}

const resultText = computed(() => {
  if (result.value === null) return "请输入字符串后点击检测是否为URL格式";
  return `isUrl("${val.value}") = ${result.value}`;
});
</script>

<template>
  <n-card title="判断是否为URL格式">
    <n-space vertical>
      <n-input v-model:value="val" placeholder="请输入URL字符串" clearable />
      <n-button type="primary" @click="checkIsUrl">检测</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
