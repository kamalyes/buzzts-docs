<script setup lang="ts">
import { ref, computed } from "vue";
import { randDate } from "buzzts";

const startYear = ref<number>(1970);
const endYear = ref<number>(new Date().getFullYear() + 10);
const dateResult = ref<Date | null>(null);

function generateRandDate() {
  dateResult.value = randDate(startYear.value, endYear.value);
}

const dateText = computed(() => {
  if (!dateResult.value) return "点击生成随机日期";
  return `randDate() = ${dateResult.value.toISOString().slice(0, 10)}`; // 只显示日期部分
});
</script>

<template>
  <n-card title="随机日期生成">
    <n-space vertical>
      <n-input-number v-model:value="startYear" :min="1900" :max="endYear" label="起始年份" />
      <n-input-number v-model:value="endYear" :min="startYear" :max="2100" label="结束年份" />

      <n-button type="primary" @click="generateRandDate">生成随机日期</n-button>

      <n-gradient-text type="info">{{ dateText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
