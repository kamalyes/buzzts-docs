<script setup lang="ts">
import { ref, computed } from 'vue';
import { isLeapYear } from 'buzzts';

const year = ref<number>(2023);
const isLeap = computed(() => {
  return isLeapYear(year.value);
});

const resultText = computed(() => {
  return `isLeapYear(${year.value}) = ${isLeap.value}`;
});

</script>

<template>
  <n-card>
    <h3>判断指定年份是否为闰年</h3>
    <n-input v-model:value="year" type="number" placeholder="输入年份" style="width: 100%; margin-bottom: 12px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
