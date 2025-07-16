<script setup lang="ts">
import { ref, computed } from "vue";
import { filterObject } from 'buzzts';

// 定义输入对象和属性数组的默认值
const inputObject = ref('{"a": 1, "b": "2", "c": 3}');
const paths = ref('a, c');
const action = ref<'pick' | 'omit'>('pick');

const actionOptions = [
  { label: '选择 (pick)', value: 'pick' },
  { label: '忽略 (omit)', value: 'omit' },
];

// 计算过滤结果
const filteredResult = computed(() => {
  try {
    const object = JSON.parse(inputObject.value); // 将输入的 JSON 字符串解析为对象
    const pathArray = paths.value.split(',').map(path => path.trim()); // 将输入的属性数组转换为数组
    return filterObject(object, pathArray, action.value); // 调用 filterObject 函数
  } catch (error) {
    return '输入的对象格式不正确'; // 错误处理
  }
});
</script>

<template>
  <n-card title="对象属性过滤器">
    <n-divider>输入对象</n-divider>
    <n-input
      v-model:value="inputObject"
      placeholder="请输入对象（JSON 格式）"
      style="width: 100%;"
    />
    
    <n-divider>属性数组</n-divider>
    <n-input
      v-model:value="paths"
      placeholder="请输入属性数组（用逗号分隔）"
      style="width: 100%;"
    />
    
    <n-divider>操作类型</n-divider>
    <n-select v-model:value="action" :options="actionOptions" style="width: 100%;" />
    
    <n-divider>过滤结果</n-divider>
    <div>{{ filteredResult }}</div>
  </n-card>
</template>

<style>
/* 可选样式 */
</style>
