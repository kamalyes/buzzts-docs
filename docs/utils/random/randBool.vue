<script setup lang="ts">
import { ref, computed } from "vue";
import { randBool } from "buzzts";

const boolResult = ref<boolean | null>(null);

function generateBool() {
  boolResult.value = randBool();
}

const resultText = computed(() => {
  if (boolResult.value === null) return "点击生成";
  return `randBool() = ${boolResult.value}`;
});
</script>

<template>
  <n-card title="随机布尔值生成">
    <n-space vertical>
      <n-button type="primary" @click="generateBool">生成随机布尔值</n-button>

      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
