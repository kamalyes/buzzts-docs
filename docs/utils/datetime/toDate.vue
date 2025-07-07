<script setup lang="ts">
import { ref, watch, computed } from 'vue';
import { toDate } from 'buzzts';
import { validDateExamples } from './constant';

interface ExampleResult {
  label: string;
  input: string;
  date: Date | null;
  valid: boolean;
}

const inputValue = ref('2023-06-23');
const parsedDate = ref<Date | null>(null);
const isValid = ref(false);
const expanded = ref(false);

function parseInput(val: string) {
  const d = toDate(val);
  parsedDate.value = d;
  isValid.value = d !== null;
}

watch(inputValue, (val) => {
  if (!expanded.value) {
    parseInput(val);
  }
}, { immediate: true });

const expandedResults = computed<ExampleResult[]>(() => {
  if (!expanded.value) return [];
  return validDateExamples.map(item => {
    const d = toDate(item.value);
    return {
      label: item.label,
      input: item.value,
      date: d,
      valid: d !== null,
    };
  });
});

function expandAll() {
  expanded.value = true;
}

function collapseAll() {
  expanded.value = false;
  parseInput(inputValue.value);
}
</script>

<template>
  <div class="buzzts-border p-4">
    <h3>toDate</h3>

    <!-- 输入选择，展开时禁用 -->
    <n-select
      v-model:value="inputValue"
      :options="validDateExamples"
      style="width: 300px"
      placeholder="选择测试案例或输入自定义"
      clearable
      filterable
      :disabled="expanded"
    />

    <!-- 输入框，展开时禁用 -->
    <n-input
      v-model:value="inputValue"
      placeholder="或输入日期字符串、时间戳等"
      style="width: 300px; margin-top: 12px"
      :disabled="expanded"
    />

    <div class="mt-4">
      <!-- 根据展开状态显示切换按钮 -->
      <n-button  type="primary" v-if="!expanded" @click="expandAll">全部展开</n-button>
      <n-button  type="primary" v-else @click="collapseAll">收起全部</n-button>
    </div>

    <!-- 单条解析结果展示 -->
    <div class="mt-4" v-if="!expanded">
      <n-tag :type="isValid ? 'success' : 'error'">
        {{ isValid ? '解析成功，返回 Date 对象' : '解析失败，返回 null' }}
      </n-tag>

      <div class="mt-2" v-if="isValid && parsedDate">
        <pre>{{ parsedDate }}</pre>
      </div>
    </div>

    <!-- 全部示例解析结果列表 -->
    <div class="mt-4" v-if="expanded">
      <div
        v-for="(item, index) in expandedResults"
        :key="index"
        style="margin-bottom: 12px; border-bottom: 1px solid #eee; padding-bottom: 8px;"
      >
        <div><strong>示例：</strong>{{ item.label }}</div>
        <div><strong>输入：</strong>{{ item.input }}</div>
        <n-tag :type="item.valid ? 'success' : 'error'">
          {{ item.valid ? '解析成功' : '解析失败' }}
        </n-tag>
        <div v-if="item.valid && item.date" style="margin-top: 4px;">
          <pre>{{ item.date }}</pre>
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
