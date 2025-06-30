<script setup lang="ts">
import { computed, ref, watch, nextTick } from "vue";
import { randFloat } from "buzzts";

const floatMin = ref(-1);
const floatMax = ref(1);
const precision = ref(4);
const floatResult = ref<number | null>(null);
const allowNegative = ref(true);
const generateCount = ref(0);
const resultStats = ref<Record<string, number>>({}); // 用字符串 key，保留小数位

// 保存之前的负数值
const lastNegativeMin = ref(-1);
const lastNegativeMax = ref(-0.5);

const performanceTest = ref({
  running: false,
  progress: 0,
  results: {
    speed: 0,       // 生成速度（次/秒）
    uniformity: 0,  // 均匀性评分（0-100）
    timeTaken: 0    // 测试耗时（毫秒）
  }
});

const MAX_RANGE_SIZE = 100000;

// 切换允许负数时保存/恢复区间
watch(allowNegative, (newVal) => {
  if (newVal) {
    floatMin.value = lastNegativeMin.value;
    floatMax.value = lastNegativeMax.value;
  } else {
    if (floatMin.value < 0) lastNegativeMin.value = floatMin.value;
    if (floatMax.value < 0) lastNegativeMax.value = floatMax.value;

    if (floatMin.value < 0) floatMin.value = 0;
    if (floatMax.value <= 0) floatMax.value = 0.1;
  }
  resetStats();
});

// 限制区间大小不超过 MAX_RANGE_SIZE
watch([floatMin, floatMax], ([newMin, newMax]) => {
  if (typeof newMin !== "number" || typeof newMax !== "number") return;
  if (newMin >= newMax) return;

  const rangeSize = newMax - newMin;
  if (rangeSize > MAX_RANGE_SIZE) {
    floatMax.value = newMin + MAX_RANGE_SIZE;
  }
  resetStats();
}, { deep: true });

function generateFloat() {
  const val = randFloat(floatMin.value, floatMax.value, precision.value);
  floatResult.value = val;

  generateCount.value++;
  const key = val.toFixed(precision.value);
  if (!resultStats.value[key]) resultStats.value[key] = 0;
  resultStats.value[key]++;
}

function resetStats() {
  generateCount.value = 0;
  resultStats.value = {};
  floatResult.value = null;
  performanceTest.value = {
    running: false,
    progress: 0,
    results: {
      speed: 0,
      uniformity: 0,
      timeTaken: 0
    }
  };
}

async function runPerformanceTest(iterations = 10000) {
  resetStats();
  await nextTick();

  const min = floatMin.value;
  const max = floatMax.value;
  if (min >= max) {
    console.warn("区间不合法，无法进行性能测试");
    return;
  }

  const batchSize = 10000;
  const batchCount = Math.ceil(iterations / batchSize);
  const tempStats: Record<string, number> = {};

  performanceTest.value.running = true;

  const startTime = performance.now();

  for (let batch = 0; batch < batchCount; batch++) {
    await new Promise<void>((resolve) => {
      setTimeout(() => {
        for (let i = 0; i < batchSize && (batch * batchSize + i) < iterations; i++) {
          const num = randFloat(min, max, precision.value);
          const key = num.toFixed(precision.value);
          floatResult.value = num;
          tempStats[key] = (tempStats[key] || 0) + 1;
        }
        resolve();
      }, 0);
    });

    performanceTest.value.progress = Math.round(((batch + 1) / batchCount) * 100);
  }

  const endTime = performance.now();

  // 计算均匀性评分（简单版，基于所有出现的结果）
  const keys = Object.keys(tempStats);
  const expected = iterations / keys.length;
  let chiSquare = 0;
  for (const key of keys) {
    const observed = tempStats[key];
    chiSquare += Math.pow(observed - expected, 2) / expected;
  }
  const uniformity = Math.max(0, 100 - chiSquare);

  // 合并统计数据
  for (const key in tempStats) {
    resultStats.value[key] = (resultStats.value[key] || 0) + tempStats[key];
  }
  generateCount.value += iterations;

  performanceTest.value = {
    running: false,
    progress: 100,
    results: {
      speed: Math.round(iterations / ((endTime - startTime) / 1000)),
      uniformity: Math.round(uniformity),
      timeTaken: Math.round(endTime - startTime)
    }
  };
}

const resultText = computed(() => {
  if (floatResult.value === null) return "点击生成";
  return `randFloat(${floatMin.value}, ${floatMax.value}, ${precision.value}) = ${floatResult.value.toFixed(precision.value)}`;
});

const possibleValues = computed(() => {
  // 生成可选值列表，保留精度
  const min = floatMin.value;
  const max = floatMax.value;
  if (min >= max) return [];

  const step = Math.pow(10, -precision.value);
  const values = [];
  for (let v = min; v <= max; v = +(v + step).toFixed(precision.value)) {
    values.push(v.toFixed(precision.value));
  }
  return values;
});

const statsTable = computed(() => {
  if (generateCount.value === 0) return [];

  const keys = Object.keys(resultStats.value).sort((a, b) => parseFloat(a) - parseFloat(b));
  return keys.map(key => {
    const count = resultStats.value[key] || 0;
    const percentage = ((count / generateCount.value) * 100).toFixed(2);
    const expected = (100 / keys.length).toFixed(2) + "%";
    return {
      value: key,
      count,
      percentage: `${percentage}%`,
      expected
    };
  });
});
</script>

<template>
  <n-card title="高精度随机浮点数生成" style="width: 100%">
    <n-space vertical>
      <n-switch v-model:value="allowNegative" class="mb-4">
        <template #checked>允许负数</template>
        <template #unchecked>仅正数</template>
      </n-switch>

      <n-space>
        <n-input-number
          v-model:value="floatMin"
          :min="allowNegative ? -Infinity : 0"
          :max="floatMax - 0.0001"
          :step="Math.pow(10, -precision)"
        />
        <n-text>最小值</n-text>
      </n-space>

      <n-space>
        <n-input-number
          v-model:value="floatMax"
          :min="floatMin + 0.0001"
          :step="Math.pow(10, -precision)"
        />
        <n-text>最大值</n-text>
      </n-space>

      <n-space>
        <n-input-number
          v-model:value="precision"
          :min="1"
          :max="16"
          :step="1"
        />
        <n-text>小数位数 (1-16)</n-text>
      </n-space>

      <n-space>
        <n-button type="primary" @click="generateFloat">生成</n-button>
        <n-button type="error" @click="resetStats">重置统计</n-button>
        <n-button
          type="info"
          @click="runPerformanceTest()"
          :disabled="performanceTest.running"
        >
          {{ performanceTest.running ? `测试中 (${performanceTest.progress}%)` : '性能测试' }}
        </n-button>
      </n-space>

      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>

      <n-card title="性能测试结果" size="small" v-if="performanceTest.results.speed > 0">
        <n-space vertical>
          <n-statistic label="生成速度" :value="performanceTest.results.speed">
            <template #suffix>次/秒</template>
          </n-statistic>
          <n-statistic label="均匀性评分" :value="performanceTest.results.uniformity">
            <template #suffix>/100</template>
          </n-statistic>
          <n-statistic label="测试耗时" :value="performanceTest.results.timeTaken">
            <template #suffix>毫秒</template>
          </n-statistic>
        </n-space>
      </n-card>

      <n-card title="概率统计" size="small" style="border-radius: 8px">
        <n-text>总生成次数: {{ generateCount }}</n-text>

        <div style="overflow-x: auto;">
          <n-data-table
            :columns="[
              { title: '数值', key: 'value', align: 'center', minWidth: 150 },
              { title: '出现次数', key: 'count', align: 'center', minWidth: 180 },
              { title: '实际概率', key: 'percentage', align: 'center', minWidth: 120 },
              { title: '理论概率', key: 'expected', align: 'center', minWidth: 120 }
            ]"
            :data="statsTable"
            :pagination="{ pageSize: 8 }"
            :bordered="false"
            class="full-width-table"
          />
        </div>
      </n-card>
    </n-space>
  </n-card>
</template>

<style scoped>
.full-width-table {
  width: 100%;
}
</style>
