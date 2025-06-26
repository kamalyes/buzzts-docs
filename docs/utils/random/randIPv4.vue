<script setup lang="ts">
import { ref, computed } from "vue";
import { randIPv4 } from "buzzts";

const result = ref<string>("");

function generateIPV4() {
  result.value = randIPv4();
}

const resultText = computed(() => {
  if (!result.value) return "点击生成IPV4";
  return `randIPV4() = ${result.value}`;
});
</script>

<template>
  <n-card title="随机IPv4地址生成">
    <n-space vertical>
      <n-button type="primary" @click="generateIPV4">生成IPv4地址</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>