<script setup lang="ts">
import { ref, computed, watch } from "vue";
import { rangeWithStep } from "buzzts";

const min = ref(3);
const max = ref(1);
const step = ref(1);
const mode = ref<'int' | 'float'>('int');

function resetValues() {
  if (mode.value === 'int') {
    min.value = 0;
    max.value = 10;
    step.value = 1;
  } else {
    min.value = 0.0;
    max.value = 10.0;
    step.value = 0.1;
  }
}

// 监听mode变化，调整数值并保证范围和步长合理
watch(mode, (newMode) => {
  resetValues();
  if (newMode === 'int') {
    // 转整数
    min.value = Math.round(min.value);
    max.value = Math.round(max.value);
    step.value = Math.round(step.value);
    if (step.value < 1) step.value = 1;
  } else {
    // 浮点模式，保留两位小数，确保是浮点数
    min.value = parseFloat(min.value.toFixed(2));
    max.value = parseFloat(max.value.toFixed(2));
    step.value = step.value < 0.01 ? 0.01 : parseFloat(step.value.toFixed(2));
  }
  if (min.value > max.value) [min.value, max.value] = [max.value, min.value];
});

// 处理参数，保证计算时类型正确
const processedMin = computed(() =>
  mode.value === 'int' ? Math.round(min.value) : min.value
);
const processedMax = computed(() =>
  mode.value === 'int' ? Math.round(max.value) : max.value
);
const processedStep = computed(() => {
  if (mode.value === 'int') {
    const s = Math.round(step.value);
    return s > 0 ? s : 1;
  }
  return step.value > 0 ? step.value : 0.1;
});

// 生成区间数组
const rangeArray = computed(() => {
  try {
    return rangeWithStep(processedMin.value, processedMax.value, processedStep.value);
  } catch {
    return [];
  }
});

const displayText = computed(() =>
  `rangeWithStep(${processedMin.value}, ${processedMax.value}, ${processedStep.value}) = [${rangeArray.value.join(", ")}]`
);
</script>

<template>
  <n-card title="规范区间生成（支持整数/浮点模式切换）">
    <n-space vertical>
      <div>
        <label>模式切换：</label>
        <n-radio-group v-model:value="mode" size="small">
          <n-radio value="int">整数模式</n-radio>
          <n-radio value="float">浮点模式</n-radio>
        </n-radio-group>
      </div>

      <div>
        <label>区间起点：{{ processedMin }}</label>
        <n-slider
          v-model:value="min"
          :min="-100"
          :max="500"
          :step="mode === 'int' ? 1 : 0.01"
          :precision="mode === 'int' ? 0 : 2"
        />
      </div>
      <div>
        <label>区间终点：{{ processedMax }}</label>
        <n-slider
          v-model:value="max"
          :min="-100"
          :max="500"
          :step="mode === 'int' ? 1 : 0.01"
          :precision="mode === 'int' ? 0 : 2"
        />
      </div>
      <div>
        <label>步长：{{ processedStep }}</label>
        <n-slider
          v-model:value="step"
          :min="mode === 'int' ? 1 : 0.01"
          :max="mode === 'int' ? 20 : 10"
          :step="mode === 'int' ? 1 : 0.01"
          :precision="mode === 'int' ? 0 : 2"
        />
      </div>

      <n-gradient-text type="info">
        {{ displayText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
