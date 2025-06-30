<script setup lang="ts">
import { computed, ref, watch, nextTick } from "vue";
import { randInt } from "buzzts";

const intMin = ref(-10);
const intMax = ref(10);
const intResult = ref<number | null>(null);
const allowNegative = ref(true);
const generateCount = ref(0);
const resultStats = ref<Record<number, number>>({});

// 保存之前的负数值
const lastNegativeMin = ref(-10);
const lastNegativeMax = ref(-5);

// 性能测试相关状态
const performanceTest = ref({
  running: false,
  progress: 0,
  results: {
    speed: 0,       // 生成速度（次/秒）
    uniformity: 0,  // 均匀性评分（0-100）
    timeTaken: 0    // 测试耗时（毫秒）
  }
});

// 当切换正负数模式时处理数值转换
watch(allowNegative, (newVal) => {
  if (newVal) {
    // 恢复之前保存的负数值
    intMin.value = lastNegativeMin.value;
    intMax.value = lastNegativeMax.value;
  } else {
    // 保存当前负数值
    if (intMin.value < 0) lastNegativeMin.value = intMin.value;
    if (intMax.value < 0) lastNegativeMax.value = intMax.value;
    
    // 转换为正数
    if (intMin.value < 0) intMin.value = 0;
    if (intMax.value < 0) intMax.value = 1;
  }
  resetStats();
});

const MAX_RANGE_SIZE = 100000;
// 监听 min/max 变化，清空统计
watch([intMin, intMax], ([newMin, newMax], [oldMin, oldMax]) => {
  if (!Number.isInteger(newMin) || !Number.isInteger(newMax)) return;
  if (newMin > newMax) return;

  const rangeSize = newMax - newMin + 1;
  if (rangeSize > MAX_RANGE_SIZE) {
    // 自动调整最大值，保证区间大小不超过 MAX_RANGE_SIZE
    intMax.value = newMin + MAX_RANGE_SIZE - 1;
  }

  // 清空统计
  resetStats();
}, { deep: true });


function generateInt() {
  resetStats();
  intResult.value = randInt(intMin.value, intMax.value);
  generateCount.value++;
  
  // 更新统计信息
  if (!resultStats.value[intResult.value]) {
    resultStats.value[intResult.value] = 0;
  }
  resultStats.value[intResult.value]++;
}

function resetStats() {
  generateCount.value = 0;
  resultStats.value = {};
  intResult.value = null;
  // 清空性能测试结果
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

  const min = intMin.value;
  const max = intMax.value;

  if (possibleValues.value.length === 0) {
    console.warn('范围不合法，无法进行性能测试');
    return;
  }

  const batchSize = 10000;
  const batchCount = Math.ceil(iterations / batchSize);
  const tempStats: Record<number, number> = {};

  const startTime = performance.now();

  for (let batch = 0; batch < batchCount; batch++) {
    // 单批异步执行
    await new Promise<void>(resolve => {
      setTimeout(() => {
        for (let i = 0; i < batchSize && (batch * batchSize + i) < iterations; i++) {
          const num = randInt(min, max);
          intResult.value = num;
          tempStats[num] = (tempStats[num] || 0) + 1;
        }
        resolve();
      }, 0);
    });

    performanceTest.value.progress = Math.round(((batch + 1) / batchCount) * 100);
  }

  // 计算均匀性
  const expected = iterations / possibleValues.value.length;
  let chiSquare = 0;
  for (const num of possibleValues.value) {
    const observed = tempStats[num] || 0;
    chiSquare += Math.pow(observed - expected, 2) / expected;
  }
  const uniformity = Math.max(0, 100 - chiSquare);

  const endTime = performance.now();

  // 合并数据
  for (const key in tempStats) {
    const k = Number(key);
    resultStats.value[k] = (resultStats.value[k] || 0) + tempStats[k];
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


const intText = computed(() => {
  if (intResult.value === null) return "点击生成";
  return `randInt(${intMin.value}, ${intMax.value}) = ${intResult.value}`;
});

const possibleValues = computed(() => {
  const min = Number(intMin.value);
  const max = Number(intMax.value);
  if (!Number.isInteger(min) || !Number.isInteger(max) || min > max) return [];
  const values = [];
  for (let i = min; i <= max; i++) {
    values.push(i);
  }
  return values;
});

const statsTable = computed(() => {
  if (generateCount.value === 0) return [];

  const keys = Object.keys(resultStats.value).map(Number).sort((a, b) => a - b);
  return keys.map(value => {
    const count = resultStats.value[value] || 0;
    const percentage = ((count / generateCount.value) * 100).toFixed(2);
    const expected = (100 / keys.length).toFixed(2) + '%';
    return {
      value,
      count,
      percentage: `${percentage}%`,
      expected
    };
  });
});
</script>

<template>
  <n-card title="随机整数生成" style="width: 100%">
    <n-space vertical>
      <n-switch v-model:value="allowNegative" class="mb-4">
        <template #checked>允许负数</template>
        <template #unchecked>仅正数</template>
      </n-switch>
      
      <n-space>
        <n-input-number 
          v-model:value="intMin" 
          :min="allowNegative ? -Infinity : 0"
          :max="intMax - 1"
        />
        <n-text>最小值</n-text>
      </n-space>
      
      <n-space>
        <n-input-number 
          v-model:value="intMax" 
          :min="intMin + 1"
        />
        <n-text>最大值</n-text>
      </n-space>
      
      <n-space>
        <n-button type="primary" @click="generateInt">生成</n-button>
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
        {{ intText }}
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
