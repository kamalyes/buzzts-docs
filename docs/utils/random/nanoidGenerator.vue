<script setup lang="ts">
import { ref, computed, nextTick } from 'vue';
import { nanoid, ALPHA_BYTES } from 'buzzts';

const size = ref(21);
const customAlpha = ref('');
const result = ref('');

// 统计相关
const generateCount = ref(0);
const resultStats = ref<Record<string, number>>({});

// 性能测试状态
const performanceTest = ref({
  running: false,
  progress: 0,
  results: {
    speed: 0,       // 次/秒
    uniformity: 0,  // 0-100
    timeTaken: 0    // 毫秒
  }
});

function generateId() {
  resetStats();
  const alphabet = customAlpha.value.trim();
  if (alphabet && alphabet.length === 0) {
    result.value = '字母表不能为空';
    return;
  }
  let id: string;
  if (alphabet) {
    id = nanoid(size.value, alphabet);
  } else {
    id = nanoid(size.value);
  }
  result.value = id;

  // 统计
  generateCount.value++;
  resultStats.value[id] = (resultStats.value[id] || 0) + 1;
}

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

async function runPerformanceTest(iterations = 10000) {
  resetStats();
  await nextTick();

  const alphabet = customAlpha.value.trim();
  const useCustom = alphabet.length > 0;

  performanceTest.value.running = true;
  performanceTest.value.progress = 0;

  const batchSize = 10000;
  const batchCount = Math.ceil(iterations / batchSize);
  const tempStats: Record<string, number> = {};

  const startTime = performance.now();

  for (let batch = 0; batch < batchCount; batch++) {
    await new Promise<void>(resolve => {
      setTimeout(() => {
        for (let i = 0; i < batchSize && (batch * batchSize + i) < iterations; i++) {
          const id = useCustom ? nanoid(size.value, alphabet) : nanoid(size.value);
          tempStats[id] = (tempStats[id] || 0) + 1;
          result.value = id;
        }
        resolve();
      }, 0);
    });
    performanceTest.value.progress = Math.round(((batch + 1) / batchCount) * 100);
  }

  const endTime = performance.now();

  // 计算均匀性评分（简单基于出现次数的方差，越小越均匀）
  const counts = Object.values(tempStats);
  const avg = iterations / counts.length;
  const variance = counts.reduce((acc, c) => acc + (c - avg) ** 2, 0) / counts.length;
  // 均匀性评分映射到0-100，方差越大评分越低
  const uniformity = Math.max(0, Math.round(100 - variance));

  // 合并统计
  for (const key in tempStats) {
    resultStats.value[key] = (resultStats.value[key] || 0) + tempStats[key];
  }
  generateCount.value += iterations;

  performanceTest.value.running = false;
  performanceTest.value.results = {
    speed: Math.round(iterations / ((endTime - startTime) / 1000)),
    uniformity,
    timeTaken: Math.round(endTime - startTime)
  };
}

const statsTable = computed(() => {
  if (generateCount.value === 0) return [];
  const keys = Object.keys(resultStats.value).sort();
  return keys.map(id => {
    const count = resultStats.value[id];
    const percentage = ((count / generateCount.value) * 100).toFixed(2);
    return {
      id,
      count,
      percentage: `${percentage}%`
    };
  });
});
</script>

<template>
  <n-card title="Nanoid 随机 ID 生成器 + 性能测试" style="max-width: 800px; margin: auto;">
    <n-space vertical size="large">
      <n-input-number
        v-model:value="size"
        label="ID 长度"
        :min="1"
        :max="64"
      />

      <n-input
        v-model:value="customAlpha"
        placeholder="自定义字母表（留空使用默认字母表）"
        clearable
      />
      <p>当前自定义字母表: {{ customAlpha || ALPHA_BYTES }}</p>

      <n-space>
        <n-button type="primary" @click="generateId">生成随机 ID</n-button>
        <n-button type="error" @click="resetStats">重置统计</n-button>
        <n-button
          type="success"
          :disabled="performanceTest.running"
          @click="runPerformanceTest()"
        >
          {{ performanceTest.running ? `性能测试中 (${performanceTest.progress}%)` : '运行性能测试（1万次）' }}
        </n-button>
      </n-space>

      <n-code style="white-space: pre-wrap; user-select: text;">
        {{ result || '点击生成随机 ID' }}
      </n-code>

      <n-card v-if="performanceTest.results.speed > 0" title="性能测试结果" size="small" bordered>
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

      <n-card v-if="generateCount > 0" title="生成统计" size="small" bordered>
        <n-text>总生成次数: {{ generateCount }}</n-text>
        <div style="overflow-x: auto;">
          <n-data-table
            :columns="[
              { title: 'ID', key: 'id', minWidth: 200 },
              { title: '出现次数', key: 'count', align: 'center', minWidth: 100 },
              { title: '实际概率', key: 'percentage', align: 'center', minWidth: 100 }
            ]"
            :data="statsTable"
            :pagination="{ pageSize: 5 }"
            :bordered="false"
            size="small"
          />
        </div>
      </n-card>
    </n-space>
  </n-card>
</template>

<style scoped>
</style>
