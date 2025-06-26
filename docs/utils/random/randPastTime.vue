<script setup lang="ts">
import { ref, computed } from "vue";
import { randPastTime } from "buzzts";

const randPastTimeResult = ref<Date | null>(null);

function generateRandPastTime() {
  randPastTimeResult.value = randPastTime();
}

const randPastTimeText = computed(() => {
  if (!randPastTimeResult.value) return "点击生成随机过去时间";
  return `randPastTime() = ${randPastTimeResult.value.toISOString()}`;
});
</script>

<template>
  <n-card title="随机过去时间生成">
    <n-space vertical>
      <n-button type="primary" @click="generateRandPastTime">生成随机过去时间</n-button>
      <n-gradient-text type="info">{{ randPastTimeText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
