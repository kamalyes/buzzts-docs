<script setup lang="ts">
import { ref, computed } from "vue";
import { randTime } from "buzzts";

const randTimeResult = ref<Date | null>(null);

function generateRandTime() {
  randTimeResult.value = randTime();
}

const randTimeText = computed(() => {
  if (!randTimeResult.value) return "点击生成随机未来时间";
  return `randTime() = ${randTimeResult.value.toISOString()}`;
});
</script>

<template>
  <n-card title="随机未来时间生成">
    <n-space vertical>
      <n-button type="primary" @click="generateRandTime">生成随机未来时间</n-button>
      <n-gradient-text type="info">{{ randTimeText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
