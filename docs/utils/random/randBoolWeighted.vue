<script setup lang="ts">
import { ref, computed, watch, nextTick } from 'vue';
import { randBoolWeighted } from 'buzzts';

const probability = ref(0.8);
const batchSize = ref(10);
const result = ref<boolean | null>(null);
const generateCount = ref(0);
const stats = ref<{ trueCount: number; falseCount: number }>({ trueCount: 0, falseCount: 0 });
const history = ref<boolean[]>([]);

const isGenerating = ref(false);
const errorMsg = ref('');

// 期望概率
const expectedTrueProb = computed(() => probability.value);
const expectedFalseProb = computed(() => 1 - probability.value);

// 真实概率
const truePercentage = computed(() => {
  if (generateCount.value === 0) return '0.00%';
  return ((stats.value.trueCount / generateCount.value) * 100).toFixed(2) + '%';
});
const falsePercentage = computed(() => {
  if (generateCount.value === 0) return '0.00%';
  return ((stats.value.falseCount / generateCount.value) * 100).toFixed(2) + '%';
});

// 误差率 = |实际概率 - 期望概率|
const trueError = computed(() => {
  if (generateCount.value === 0) return '0.00%';
  return (Math.abs((stats.value.trueCount / generateCount.value) - expectedTrueProb.value) * 100).toFixed(2) + '%';
});
const falseError = computed(() => {
  if (generateCount.value === 0) return '0.00%';
  return (Math.abs((stats.value.falseCount / generateCount.value) - expectedFalseProb.value) * 100).toFixed(2) + '%';
});

function validateInputs() {
  if (probability.value < 0 || probability.value > 1) {
    errorMsg.value = '概率 p 必须在 0 到 1 之间';
    return false;
  }
  if (batchSize.value < 1 || batchSize.value > 10000) {
    errorMsg.value = '批量生成次数必须在 1 到 10000 之间';
    return false;
  }
  errorMsg.value = '';
  return true;
}

const resultText = computed(() => {
  if (result.value === null) return '点击批量生成';
  return `randBoolWeighted(p=${probability.value.toFixed(2)}) = ${result.value ? 'true' : 'false'}`;
});


async function generateBatch() {
  resetStats()
  if (!validateInputs()) return;
  isGenerating.value = true;

  const batch = batchSize.value;
  const chunkSize = 1000; // 每次生成1000条，大小可调节
  let trueCountInc = 0;
  let falseCountInc = 0;
  let newHistory: boolean[] = [];

  for (let start = 0; start < batch; start += chunkSize) {
    const end = Math.min(start + chunkSize, batch);
    for (let i = start; i < end; i++) {
      const val = randBoolWeighted(probability.value);
      result.value = val; // 只记录最后一个结果

      if (val) trueCountInc++;
      else falseCountInc++;

      newHistory.unshift(val);
    }

    // 累计更新响应式数据
    generateCount.value += (end - start);
    stats.value.trueCount += trueCountInc;
    stats.value.falseCount += falseCountInc;

    // 合并历史，限制长度
    history.value = [...newHistory, ...history.value].slice(0, 100);

    // 重置临时计数
    trueCountInc = 0;
    falseCountInc = 0;
    newHistory = [];

    // 让出主线程，避免卡顿
    await nextTick();
  }

  isGenerating.value = false;
}

function resetStats() {
  generateCount.value = 0;
  stats.value = { trueCount: 0, falseCount: 0 };
  result.value = null;
  history.value = [];
  errorMsg.value = '';
}

const statsTable = computed(() => [
  {
    state: 'true',
    count: stats.value.trueCount,
    percentage: truePercentage.value,
    expected: (expectedTrueProb.value * 100).toFixed(2) + '%',
    error: trueError.value
  },
  {
    state: 'false',
    count: stats.value.falseCount,
    percentage: falsePercentage.value,
    expected: (expectedFalseProb.value * 100).toFixed(2) + '%',
    error: falseError.value
  }
]);

</script>

<template>
  <n-card title="概率加权随机布尔生成" style="width: 100%; max-width: 600px;">
    <n-space vertical size="large">

      <n-form :model="{ probability, batchSize }" :rules="{
        probability: [{ type: 'number', min: 0, max: 1, message: '概率 p 必须在 0 到 1 之间', trigger: 'blur' }],
        batchSize: [{ type: 'number', min: 1, max: 10000, message: '批量生成次数在 1 到 10000 之间', trigger: 'blur' }]
      }">
        <n-form-item label="概率 p (0~1)" path="probability">
          <n-slider
            v-model:value="probability"
            :min="0"
            :max="1"
            :step="0.01"
            show-tooltip
            style="width: 100%"
          />
          <n-input-number
            v-model:value="probability"
            :min="0"
            :max="1"
            :step="0.01"
            style="width: 120px; margin-top: 8px;"
          />
        </n-form-item>

        <n-form-item label="批量生成次数" path="batchSize">
          <n-input-number
            v-model:value="batchSize"
            :min="1"
            :max="10000"
            :step="1"
            style="width: 120px"
          />
        </n-form-item>
      </n-form>

      <n-space>
        <n-button :disabled="isGenerating" @click="generateBatch" type="primary">批量生成</n-button>
        <n-button :disabled="isGenerating && generateCount === 0" @click="resetStats" type="error">重置统计</n-button>
      </n-space>

      <n-alert v-if="errorMsg" type="error" :closable="false" :title="errorMsg" />

      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>

     <n-card title="概率统计" size="small" style="border-radius: 8px;">
      <n-text style="display: block; margin-bottom: 12px;">总生成次数: {{ generateCount }}</n-text>
        <div style="overflow-x: auto;">
          <n-data-table
            :columns="[
              { title: '状态', key: 'state', align: 'center', minWidth: 100 },
              { title: '出现次数', key: 'count', align: 'center', minWidth: 120 },
              { title: '实际概率', key: 'percentage', align: 'center', minWidth: 120 },
              { title: '理论概率', key: 'expected', align: 'center', minWidth: 120 },
              { title: '概率误差', key: 'error', align: 'center', minWidth: 120 }
            ]"
            :data="statsTable"
            :pagination="{ pageSize: 8 }"
            :bordered="false"
            class="full-width-table"
          />
        </div>
      </n-card>

      <n-card
        title="最近生成结果（最新在前）"
        size="small"
        style="border-radius: 8px; max-height: 120px; overflow-y: auto;"
      >
        <n-space wrap>
          <n-tag
            v-for="(val, index) in history"
            :key="index"
            :type="val ? 'success' : 'error'"
          >
            {{ val ? 'true' : 'false' }}
          </n-tag>
        </n-space>
      </n-card>

    </n-space>
  </n-card>
</template>
<style scoped>
.full-width-table {
  width: 100%;
}
</style>