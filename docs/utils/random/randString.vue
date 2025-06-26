<script setup lang="ts">
import { ref, computed, watch, nextTick } from 'vue';
import { RandType, randString } from 'buzzts';

// --- 基础参数 ---
const length = ref(10);
const selectedTypes = ref<string[]>(['capital', 'number']);
const result = ref('');

// 计算模式掩码
const mode = computed(() => {
  let m = 0;
  if (selectedTypes.value.includes('capital')) m |= RandType.CAPITAL;
  if (selectedTypes.value.includes('lowercase')) m |= RandType.LOWERCASE;
  if (selectedTypes.value.includes('special')) m |= RandType.SPECIAL;
  if (selectedTypes.value.includes('number')) m |= RandType.NUMBER;
  return m;
});

// 生成随机字符串
function generate() {
  resetStats();
  if (length.value <= 0) {
    result.value = '';
    return;
  }
  if (mode.value === 0) {
    result.value = '请至少选择一种字符类型';
    return;
  }
  result.value = randString(length.value, mode.value);
}

// --- 性能测试相关状态 ---
const generateCount = ref(0);
const resultStats = ref<Record<string, number>>({});

const performanceTest = ref({
  running: false,
  progress: 0,
  results: {
    speed: 0,       // 生成速度（次/秒）
    uniformity: 0,  // 均匀性评分（0-100）
    timeTaken: 0    // 测试耗时（毫秒）
  }
});

// 重置统计数据
function resetStats() {
  generateCount.value = 0;
  resultStats.value = {};
  result.value = '';
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

// 生成所有可能字符集合（根据选中的类型）
const charSets = {
  capital: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
  lowercase: 'abcdefghijklmnopqrstuvwxyz',
  number: '0123456789',
  special: '.@$!%*#_~?&^'
};
const possibleChars = computed(() => {
  let chars = '';
  if (selectedTypes.value.includes('capital')) chars += charSets.capital;
  if (selectedTypes.value.includes('lowercase')) chars += charSets.lowercase;
  if (selectedTypes.value.includes('number')) chars += charSets.number;
  if (selectedTypes.value.includes('special')) chars += charSets.special;
  return chars;
});

const resultText = computed(() => {
  if (!result.value) return '点击生成随机数字字符串';
  return `randString(${length.value},${mode.value}) = ${result.value}`;
});

// 性能测试函数，默认测试10000次
async function runPerformanceTest(iterations = 10000) {
  if (length.value <= 0 || mode.value === 0) {
    alert('请先设置有效的长度和字符类型');
    return;
  }
  if (possibleChars.value.length === 0) {
    alert('无有效字符集，无法测试');
    return;
  }

  resetStats();
  await nextTick();

  performanceTest.value.running = true;
  performanceTest.value.progress = 0;

  const batchSize = 1000;
  const batchCount = Math.ceil(iterations / batchSize);
  const tempStats: Record<string, number> = {};

  const startTime = performance.now();

  for (let batch = 0; batch < batchCount; batch++) {
    await new Promise<void>((resolve) => {
      setTimeout(() => {
        for (let i = 0; i < batchSize && (batch * batchSize + i) < iterations; i++) {
          const str = randString(length.value, mode.value);
          tempStats[str] = (tempStats[str] || 0) + 1;
          result.value = str;
        }
        resolve();
      }, 0);
    });
    performanceTest.value.progress = Math.round(((batch + 1) / batchCount) * 100);
  }

  const endTime = performance.now();

  // 计算均匀性（卡方检验）
  // 理论上所有字符串出现概率应该均等，但字符串空间巨大，实际计算卡方不现实
  // 这里简化为根据字符集大小和长度计算理论总可能数，并用出现次数统计字符串数目
  // 只统计出现过的字符串，均匀性评分意义有限，给出简单评分
  const totalPossible = Math.pow(possibleChars.value.length, length.value);
  const observedCount = Object.keys(tempStats).length;
  // 简单均匀性评分：出现不同字符串比例 * 100，越接近1越均匀
  const uniformity = Math.min(100, (observedCount / iterations) * 100);

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

// 统计表格数据，显示出现次数和概率
const statsTable = computed(() => {
  if (generateCount.value === 0) return [];
  const keys = Object.keys(resultStats.value).sort();
  return keys.map(key => {
    const count = resultStats.value[key];
    const percentage = ((count / generateCount.value) * 100).toFixed(2);
    return {
      value: key,
      count,
      percentage: `${percentage}%`
    };
  });
});
</script>

<template>
  <n-card title="随机字符串生成" style="width: 100%; max-width: 600px;">
    <n-space vertical>
      <n-input-number v-model:value="length" :min="1" label="长度" />

      <n-checkbox-group v-model:value="selectedTypes">
        <n-checkbox value="capital">大写字母 (A-Z)</n-checkbox>
        <n-checkbox value="lowercase">小写字母 (a-z)</n-checkbox>
        <n-checkbox value="special">特殊字符 (.@$!%*#_~?&^)</n-checkbox>
        <n-checkbox value="number">数字 (0-9)</n-checkbox>
      </n-checkbox-group>

      <n-button type="primary" @click="generate" :disabled="performanceTest.running">生成随机字符串</n-button>
      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>

      <n-button 
        type="success" 
        @click="runPerformanceTest()" 
        :loading="performanceTest.running"
      >
        {{ performanceTest.running ? `测试中 (${performanceTest.progress}%)` : '性能测试（1万次）' }}
      </n-button>

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

      <n-card title="概率统计" size="small" style="border-radius: 8px" v-if="generateCount > 0">
        <n-text>总生成次数: {{ generateCount }}</n-text>

        <div style="overflow-x: auto;">
          <n-data-table
            :columns="[
              { title: '字符串', key: 'value', align: 'center', minWidth: 200 },
              { title: '出现次数', key: 'count', align: 'center', minWidth: 150 },
              { title: '实际概率', key: 'percentage', align: 'center', minWidth: 150 }
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
