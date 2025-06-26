<script setup lang="ts">
import { ref, computed } from "vue";
import { randISOTime } from "buzzts";

const isoResult = ref<string | null>(null);

function generateRandISOTime() {
  isoResult.value = randISOTime();
}

const isoText = computed(() => {
  if (!isoResult.value) return "点击生成随机 ISO 时间";
  return `randISOTime() = ${isoResult.value}`;
});
</script>

<template>
  <n-card title="随机 ISO 时间生成">
    <n-space vertical>
      <n-button type="primary" @click="generateRandISOTime">生成随机 ISO 时间</n-button>
      <n-gradient-text type="info">{{ isoText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
