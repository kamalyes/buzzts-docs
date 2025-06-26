<script setup lang="ts">
import { ref, computed } from "vue";
import { randTimeBetween } from "buzzts";

const now = new Date();
const range = ref<[Date | null, Date | null]>([
  new Date(now.getTime() - 1 * 24 * 3600 * 1000), // 当前时间减1天
  new Date(now.getTime() + 6 * 24 * 3600 * 1000), // 当前时间加6天
]);

const betweenResult = ref<Date | null>(null);
const errorMsg = ref("");

function generateRandBetween() {
  errorMsg.value = "";
  betweenResult.value = null;

  const [start, end] = range.value;

  if (!start || !end) {
    errorMsg.value = "请选择有效的开始和结束时间";
    return;
  }

  if (!(start instanceof Date) || !(end instanceof Date)) {
    errorMsg.value = "开始和结束时间必须是有效的日期对象";
    return;
  }

  if (isNaN(start.getTime()) || isNaN(end.getTime())) {
    errorMsg.value = "请选择有效的开始和结束时间";
    return;
  }

  if (start > end) {
    errorMsg.value = "开始时间不能晚于结束时间";
    return;
  }

  // 这里调用你生成随机时间的函数
  betweenResult.value = randTimeBetween(start, end);
}

const betweenText = computed(() => {
  if (errorMsg.value) return `错误: ${errorMsg.value}`;
  if (!betweenResult.value || isNaN(betweenResult.value.getTime())) return "点击生成区间随机时间";
  return `randTimeBetween() = ${betweenResult.value.toISOString()}`;
});
</script>

<template>
  <n-card title="区间随机时间生成">
    <n-space vertical size="large">
      <n-date-picker
        v-model:value="range"
        type="datetimerange"
        placeholder="请选择开始和结束时间"
        clearable
        format="yyyy-MM-dd HH:mm"
        :value-format="'yyyy-MM-ddTHH:mm:ss'"
        :time-picker-options="{ start: '00:00', step: '00:01', end: '23:59' }"
      />
      <n-button type="primary" @click="generateRandBetween">生成区间随机时间</n-button>

      <n-text :type="errorMsg ? 'error' : 'success'">{{ betweenText }}</n-text>
    </n-space>
  </n-card>
</template>
