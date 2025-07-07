<script setup lang="ts">
import { ref, watch, computed } from 'vue';
import { addTime } from 'buzzts';

// 单条输入相关
const inputValue = ref<string | null>('2023-06-23T00:00:00+08:00');
const unit = ref<'date' | 'hours' | 'minutes' | 'seconds'>('date');
const amount = ref(1);

const resultDate = ref<Date | null>(null);
const isValid = ref(false);

function calculate() {
  if (!inputValue.value) {
    resultDate.value = null;
    isValid.value = false;
    return;
  }
  const res = addTime(inputValue.value, amount.value, unit.value);
  resultDate.value = res;
  isValid.value = res !== null;
}

watch([inputValue, unit, amount], calculate, { immediate: true });

// 示例数据，这里只存单位和数量，输入统一用 inputValue
const exampleConfigs = [
  { label: '加 1 天', unit: 'date', amount: 1 },
  { label: '减 5 小时', unit: 'hours', amount: -5 },
  { label: '加 30 分钟', unit: 'minutes', amount: 30 },
  { label: '加 120 秒', unit: 'seconds', amount: 120 },
];

const expanded = ref(false);

interface ExampleResult {
  label: string;
  input: string | null;
  unit: string;
  amount: number;
  result: Date | null;
  valid: boolean;
}
const expandedResults = ref<ExampleResult[]>([]);

function expandAll() {
  if (!inputValue.value) {
    expandedResults.value = [];
    expanded.value = true;
    return;
  }
  expanded.value = true;
  expandedResults.value = exampleConfigs.map(item => {
    const res = addTime(inputValue.value!, item.amount, item.unit as any);
    return {
      label: item.label,
      input: inputValue.value,
      unit: item.unit,
      amount: item.amount,
      result: res,
      valid: res !== null,
    };
  });
}

function collapseAll() {
  expanded.value = false;
  calculate();
}

const resultText = computed(() => {
  if (resultDate.value === null) return "输入日期无效，请重新输入";
  return `addTime(${inputValue.value ?? 'null'}, ${amount.value}, ${unit.value}) = ${resultDate.value}`;
});
</script>

<template>
  <div class="buzzts-border p-4" style="max-width: 500px;">
    <h3>日期加时间示例</h3>

    <!-- 单条输入区域，展开时禁用 -->
    <n-date-picker
      v-model:value="inputValue"
      type="datetime"
      value-format="yyyy-MM-dd'T'HH:mm:ss"
      placeholder="选择日期和时间"
      clearable
      style="width: 100%; margin-bottom: 12px;"
      :disabled="expanded"
    />

    <n-select
      v-model:value="unit"
      :options="[
        { label: '天 (date)', value: 'date' },
        { label: '小时 (hours)', value: 'hours' },
        { label: '分钟 (minutes)', value: 'minutes' },
        { label: '秒 (seconds)', value: 'seconds' }
      ]"
      style="width: 100%; margin-bottom: 12px;"
      :disabled="expanded"
    />

    <n-input-number
      v-model:value="amount"
      placeholder="输入增加数量（可为负数）"
      style="width: 100%; margin-bottom: 12px;"
      :min="-100000"
      :max="100000"
      :disabled="expanded"
    />

    <!-- 展开/收起按钮 -->
    <div class="mb-4">
      <n-button type="primary" v-if="!expanded" @click="expandAll">全部展开</n-button>
      <n-button type="primary" v-else @click="collapseAll">收起全部</n-button>
    </div>

    <!-- 单条结果展示 -->
    <div v-if="!expanded">
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </div>

    <!-- 全部示例结果 -->
    <div v-else>
      <div
        v-for="(item, index) in expandedResults"
        :key="index"
        style="margin-bottom: 16px; border-bottom: 1px solid #eee; padding-bottom: 8px;"
      >
        <div><strong>{{ item.label }}</strong></div>
        <div>输入日期：{{ item.input }}</div>
        <div>单位：{{ item.unit }}</div>
        <div>数量：{{ item.amount }}</div>
        <n-tag :type="item.valid ? 'success' : 'error'">
          {{ item.valid ? '解析成功' : '解析失败' }}
        </n-tag>
        <div v-if="item.valid && item.result" style="margin-top: 6px;">
          结果：<pre style="white-space: nowrap; overflow-x: auto;">{{ item.result }}</pre>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.buzzts-border {
  border: 1px solid #d9d9d9;
  border-radius: 4px;
}
</style>
