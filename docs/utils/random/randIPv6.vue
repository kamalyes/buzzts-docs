<script setup lang="ts">
import { ref, computed } from "vue";
import { randIPv6 } from "buzzts";

const result = ref<string>("");

function generateIPV6() {
  result.value = randIPv6();
}

const resultText = computed(() => {
  if (!result.value) return "点击生成IPV6";
  return `randIPV6() = ${result.value}`;
});
</script>

<template>
  <n-card title="随机IPv6地址生成">
    <n-space vertical>
      <n-button type="primary" @click="generateIPV6">生成IPv6地址</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>