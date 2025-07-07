<script setup lang="ts">
import { ref, computed } from 'vue';
import { getBoundaryOfDay } from 'buzzts';

const inputDate = ref<Date | null>(new Date());

const start = computed(() => (inputDate.value ? getBoundaryOfDay(inputDate.value, 'start') : null));
const end = computed(() => (inputDate.value ? getBoundaryOfDay(inputDate.value, 'end') : null));

const isValidStart = computed(() => start.value !== null);
const isValidEnd = computed(() => end.value !== null);
</script>

<template>
  <div class="buzzts-border p-4" style="max-width: 400px;">
    <h3>日期边界计算示例</h3>

    <n-date-picker
      v-model:value="inputDate"
      type="datetime"
      value-format="yyyy-MM-dd'T'HH:mm:ss"
      placeholder="选择日期和时间"
      clearable
      style="width: 100%; margin-bottom: 16px;"
    />

    <n-space vertical size="medium">
      <n-space align="center" size="small">
        <n-tag :type="isValidStart ? 'success' : 'error'"> {{ isValidStart ? '当天开始时间' : '无效日期' }} </n-tag>
        <pre v-if="isValidStart" class="time-display">{{ start?.toLocaleString() }}</pre>
      </n-space>

      <n-space align="center" size="small">
        <n-tag :type="isValidEnd ? 'success' : 'error'"> {{ isValidEnd ? '当天结束时间' : '无效日期' }} </n-tag>
        <pre v-if="isValidEnd" class="time-display">{{ end?.toLocaleString() }}</pre>
      </n-space>
    </n-space>
  </div>
</template>

<style scoped>
.buzzts-border {
  border: 1px solid #d9d9d9;
  border-radius: 4px;
}

pre.time-display {
  background-color: #f5f5f5;
  padding: 6px 12px;
  border-radius: 4px;
  user-select: all;
  margin: 0;
  font-family: monospace;
  white-space: nowrap;
}
</style>
