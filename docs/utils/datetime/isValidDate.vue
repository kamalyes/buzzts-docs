<script setup lang="ts">
import { ref, watch, h } from 'vue';
import { isValidDate } from 'buzzts';
import { validDateExamples } from './constant';

interface ExampleResult {
  label: string;
  input: string;
  date: Date | null;
  valid: boolean;
}

const inputValue = ref('2023-06-23');
const isValid = ref(false);
const parsedDate = ref<Date | null>(null);

const expanded = ref(false);
const expandedResults = ref<ExampleResult[]>([]);

function checkDate(val: string) {
  const date = new Date(val);
  if (isValidDate(date)) {
    isValid.value = true;
    parsedDate.value = date;
  } else {
    isValid.value = false;
    parsedDate.value = null;
  }
}

watch(inputValue, (val) => {
  if (!expanded.value) checkDate(val);
});

checkDate(inputValue.value);

function expandAll() {
  expanded.value = true;
  expandedResults.value = validDateExamples.map(item => {
    const date = new Date(item.value);
    const valid = isValidDate(date);
    return {
      label: item.label,
      input: item.value,
      date: valid ? date : null,
      valid,
    };
  });
}

function collapseAll() {
  expanded.value = false;
  checkDate(inputValue.value);
}

const columns = [
  { title: '示例名称', key: 'label' },
  { title: '输入值', key: 'input', render: (row: ExampleResult) => h('code', row.input) },
  {
    title: '是否有效',
    key: 'valid',
    render: (row: ExampleResult) => (row.valid ? '有效' : '无效'),
  },
  {
    title: '解析结果 (ISO 格式)',
    key: 'date',
    render: (row: ExampleResult) => (row.date ? row.date.toISOString() : '-'),
  },
];
</script>

<template>
  <div class="buzzts-border p-4" style="max-width: 650px;">
    <h3>isValidDate</h3>

    <n-space vertical size="large">
      <n-select
        v-model:value="inputValue"
        :options="validDateExamples"
        style="width: 300px"
        placeholder="选择测试案例或输入自定义"
        clearable
        filterable
        :disabled="expanded"
      />

      <n-input
        v-model:value="inputValue"
        placeholder="或输入日期字符串或时间戳"
        style="width: 300px"
        :disabled="expanded"
      />

      <n-space>
        <n-button type="primary" v-if="!expanded" @click="expandAll">全部展开</n-button>
        <n-button type="primary" v-else @click="collapseAll">收起</n-button>
      </n-space>

      <div v-if="!expanded">
        <n-tag :type="isValid ? 'success' : 'error'">
          {{ isValid ? '有效的日期对象' : '无效的日期' }}
        </n-tag>
        <pre v-if="isValid" class="iso-pre">{{ parsedDate?.toISOString() }}</pre>
      </div>

      <n-data-table
        v-else
        :columns="columns"
        :data="expandedResults"
        size="small"
        bordered
      />
    </n-space>
  </div>
</template>

<style scoped>
.buzzts-border {
  border: 1px solid #d9d9d9;
  border-radius: 4px;
}

.iso-pre {
  background-color: #f5f5f5;
  padding: 6px 12px;
  border-radius: 4px;
  user-select: all;
  margin: 0;
  font-family: monospace;
  white-space: nowrap;
}
</style>
