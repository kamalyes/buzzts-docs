<script setup lang="ts">
import { ref, computed } from 'vue';
import { getYear, getMonth, getDay, getHours, getMinutes, getSeconds, getMilliseconds } from 'buzzts';

const dateInput = ref<string>('2023-06-23T15:30:55.123');

const year = computed(() => getYear(dateInput.value));
const month = computed(() => getMonth(dateInput.value));
const day = computed(() => getDay(dateInput.value));
const hours = computed(() => getHours(dateInput.value));
const minutes = computed(() => getMinutes(dateInput.value));
const seconds = computed(() => getSeconds(dateInput.value));
const milliseconds = computed(() => getMilliseconds(dateInput.value));

const resultText = computed(() => {
  return `getYear(${dateInput.value}) = ${year.value}
getMonth(${dateInput.value}) = ${month.value}
getDay(${dateInput.value}) = ${day.value} 
getHours(${dateInput.value}) = ${hours.value} 
getMinutes(${dateInput.value}) = ${minutes.value} 
getSeconds(${dateInput.value}) = ${seconds.value} 
getMilliseconds(${dateInput.value}) = ${milliseconds.value}`;
});

</script>

<template>
  <n-card title="日期时间信息">
    <n-date-picker
      v-model:value="dateInput"
      type="datetime"
      format="yyyy-MM-dd HH:mm:ss"
      placeholder="请选择日期时间"
      style="width: 100%;"
      clearable
      :show-time="true"
      :time-picker-props="{ format: 'HH:mm:ss' }"
    />
    <n-gradient-text type="info" style="white-space: pre-wrap;">{{ resultText }}</n-gradient-text>
    <n-space size="small" justify="space-between" style="margin-top: 12px; flex-wrap: wrap;">
      <n-tag size="small" type="info">年: {{ year !== null ? year : '无效' }}</n-tag>
      <n-tag size="small" type="info">月: {{ month !== null ? month : '无效' }}</n-tag>
      <n-tag size="small" type="info">日: {{ day !== null ? day : '无效' }}</n-tag>
      <n-tag size="small" type="info">时: {{ hours !== null ? hours : '无效' }}</n-tag>
      <n-tag size="small" type="info">分: {{ minutes !== null ? minutes : '无效' }}</n-tag>
      <n-tag size="small" type="info">秒: {{ seconds !== null ? seconds : '无效' }}</n-tag>
      <n-tag size="small" type="info">毫秒: {{ milliseconds !== null ? milliseconds : '无效' }}</n-tag>
    </n-space>
  </n-card>
</template>