<script setup lang="ts">
import { ref, computed } from "vue";
import { filterString } from 'buzzts';

const filteredString = ref("Hello, World!");
const sepString = ref('*');
const startIndex = ref(5);
const endIndex = ref(10);

// 计算过滤结果
const filteredResult = computed(() => filterString(filteredString.value, sepString.value, startIndex.value, endIndex.value));
</script>

<template>
  <n-card title="指定范围内字符替换">
    <n-divider>待替换文本</n-divider>
    <div>
      <n-input
        v-model:value="filteredString"
        style="width: 100%;"
        placeholder="请输入待替换文本..."
      />
    </div>
    <div>
      <strong>分隔符：</strong>
      <n-input
        v-model:value="sepString"
        style="width: 100%;"
        placeholder="请输入分隔符..."
      />
    </div>
    <div>
      <strong>开始索引：</strong>
      <n-input
        type="number"
        v-model:value="startIndex"
        style="width: 100%;"
        placeholder="请输入开始索引..."
      />
    </div>
    <div>
      <strong>结束索引：</strong>
      <n-input
        type="number"
        v-model:value="endIndex"
        style="width: 100%;"
        placeholder="请输入结束索引..."
      />
    </div>
    <n-divider>过滤结果</n-divider>
    <div>{{ filteredResult }}</div>
  </n-card>
</template>
