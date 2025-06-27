<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { randUniqueSample, rangeWithStep } from "buzzts";

// 先用 rangeWithStep 生成数字数组，再转成字符串初始化arrayText
const timestampSeconds = Math.floor(Date.now() / 1000);
const initialArray = randUniqueSample(rangeWithStep(-300, -20, 1), 10 % timestampSeconds);
const arrayText = ref<string>(initialArray.join(","));
const n = ref(2);
const batchCount = ref(100000);
const pageSize = ref(20);

type BatchResult = {
  samples: string[];
  hasDuplicate: boolean;
  error?: string;
};

const batchResults = ref<BatchResult[]>([]);
const isRunning = ref(false);
const progress = ref(0);

// 解析并校验源数组
const sourceArray = computed(() => {
  return arrayText.value
    .split(",")
    .map(s => s.trim())
    .filter(s => s !== "");
});

// 限制 n 不超过源数组长度
watch(sourceArray, (newArr) => {
  if (n.value > newArr.length) {
    n.value = newArr.length;
  }
});
const isPaused = ref(false);

// 运行批量抽样测试，分批异步执行防卡顿
async function runBatchTest() {
  if (n.value <= 0) {
    alert("抽样数量必须大于0");
    return;
  }
  if (n.value > sourceArray.value.length) {
    alert("抽样数量不能超过源数组长度");
    return;
  }
  batchResults.value = [];
  singleSampleResult.value = null;
  isRunning.value = true;
  isPaused.value = false;
  progress.value = 0;

  const batchSize = 1000;
  const total = batchCount.value;

  outerLoop: for (let start = 0; start < total; start += batchSize) {
    if (isPaused.value) break;
    const end = Math.min(start + batchSize, total);
    for (let i = start; i < end; i++) {
      if (isPaused.value) break outerLoop;
      try {
        const samples = randUniqueSample(sourceArray.value, n.value);
        const hasDuplicate = new Set(samples).size !== samples.length;
        batchResults.value.push({ samples, hasDuplicate });
        singleSampleResult.value = { samples, hasDuplicate };
      } catch (e: any) {
        batchResults.value.push({ samples: [], hasDuplicate: true, error: e?.message ?? "未知错误" });
      }
      progress.value = i + 1;
    }
    await new Promise(resolve => setTimeout(resolve, 0));
  }
  isRunning.value = false;
}

// 停止批量测试的函数，和暂停区分
function stopBatchTest() {
  if (isRunning.value) {
    isPaused.value = true;
  }
}

function pauseBatchTest() {
  if (isRunning.value) {
    isPaused.value = true;
  }
}

async function clearResults() {
  // 先停止执行
  stopBatchTest();

  // 等待异步循环结束（轮询等待 isRunning 变 false）
  while (isRunning.value) {
    await new Promise(resolve => setTimeout(resolve, 50));
  }

  // 清空数据和状态
  batchResults.value = [];
  singleSampleResult.value = null;
  progress.value = 0;
  isPaused.value = false;
  currentPage.value = 1;
}

// 重复和错误结果
const duplicates = computed(() => batchResults.value.filter(r => r.hasDuplicate || r.error));
// 无重复且无错误结果
const noDuplicates = computed(() => batchResults.value.filter(r => !r.hasDuplicate && !r.error));

// 结果排序，重复/错误优先
const sortedResults = computed(() => [...duplicates.value, ...noDuplicates.value]);

// 分页计算
const currentPage = ref(1);
const pageCount = computed(() => Math.ceil(sortedResults.value.length / pageSize.value));
const pagedResults = computed(() => {
  const start = (currentPage.value - 1) * pageSize.value;
  return sortedResults.value.slice(start, start + pageSize.value);
});

// 统计重复和错误次数
const duplicateCount = computed(() => duplicates.value.length);
const errorCount = computed(() => duplicates.value.filter(r => r.error).length);

const batchSummary = computed(() => {
  if (batchResults.value.length === 0) {
    return "尚未执行批量测试";
  }
  return `共执行 ${batchCount.value} 次批量抽样，重复次数（含错误）: ${duplicateCount.value}，错误次数: ${errorCount.value}`;
});

// 分页页码改变时滚动到顶部
onMounted(() => {
  watch(currentPage, () => {
    const container = document.querySelector("#results-container");
    if (container) container.scrollTop = 0;
  });
});

function onPageSizeChange(val: number) {
  currentPage.value = 1;
  pageSize.value = val;
}

const singleSampleResult = ref<BatchResult | null>(null);

function runSingleTest() {
  if (n.value <= 0) {
    alert("抽样数量必须大于0");
    return;
  }
  if (n.value > sourceArray.value.length) {
    alert("抽样数量不能超过源数组长度");
    return;
  }
  // 运行单次测试时，清空批量测试结果
  batchResults.value = [];
  try {
    const samples = randUniqueSample(sourceArray.value, n.value);
    const hasDuplicate = new Set(samples).size !== samples.length;
    singleSampleResult.value = { samples, hasDuplicate };
  } catch (e: any) {
    singleSampleResult.value = { samples: [], hasDuplicate: true, error: e?.message ?? "未知错误" };
  }
}

const resultText = computed(() => {
  if (!singleSampleResult.value) return "点击随机抽样";
  return `randUniqueSample([${sourceArray.value}],${n.value}) = [${singleSampleResult.value.samples}]`;
});

</script>

<template>
  <n-card title="支持10万次批量抽样分页展示（重复结果优先）" style="max-width: 900px; margin: auto;">
    <n-space vertical>
      <n-input
        v-model:value="arrayText"
        label="源数组 (逗号分隔)"
        placeholder="请输入逗号分隔的元素"
      />
      <n-input-number
        v-model:value="n"
        :min="1"
        :max="sourceArray.length"
        label="抽样数量"
      />
      <n-input-number
        v-model:value="batchCount"
        :min="1"
        :max="1000000"
        label="批次数"
      />
      <n-space align="center" style="margin-bottom: 12px;">
        <n-button :disabled="isRunning" type="info" @click="runSingleTest">
          单次抽样测试
        </n-button>

        <n-button v-if="!isRunning" type="primary" @click="runBatchTest">
          开始批量测试
        </n-button>
        <n-button v-else type="warning" @click="pauseBatchTest">
          运行中... {{ progress }}/{{ batchCount }}
        </n-button>

        <n-button type="error" @click="clearResults"> 清空结果 </n-button>
      </n-space>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>

      <div v-if="batchResults" style="margin-top: 16px; font-weight: bold;">
        {{ isRunning ? `运行中... ${progress}/${batchCount}` : batchSummary }}
      </div>

      <!-- 单次测试结果 -->
      <div v-if="!batchResults" style="margin-bottom: 12px;">
        <strong>单次测试结果：</strong>
        <span :style="{ color: singleSampleResult.hasDuplicate || singleSampleResult.error ? 'red' : 'green' }">
          <template v-if="singleSampleResult.error">
            错误：{{ singleSampleResult.error }}
          </template>
          <template v-else>
            [{{ singleSampleResult.samples.join(", ") }}] — {{ singleSampleResult.hasDuplicate ? "⚠️ 有重复" : "✔️ 无重复" }}
          </template>
        </span>
      </div>

      <!-- 批量测试结果分页 -->
      <div v-if="batchResults.length > 0" id="results-container" style="max-height: 400px; overflow-y: auto;">
        <div
          v-for="(res, idx) in pagedResults"
          :key="(currentPage - 1) * pageSize + idx"
          style="margin-bottom: 6px;"
        >
          <strong>第 {{ (currentPage - 1) * pageSize + idx + 1 }} 次：</strong>
          <span :style="{ color: res.hasDuplicate || res.error ? 'red' : 'green' }">
            <template v-if="res.error">
              错误：{{ res.error }}
            </template>
            <template v-else>
              [{{ res.samples.join(", ") }}] — {{ res.hasDuplicate ? "⚠️ 有重复" : "✔️ 无重复" }}
            </template>
          </span>
        </div>
      </div>

      <n-pagination
        v-model:page="currentPage"
        :page-count="pageCount"
        :page-size="pageSize"
        :show-size-picker="true"
        :page-sizes="[20, 50, 100]"
        @update:page-size="onPageSizeChange"
      />
    </n-space>
  </n-card>
</template>
