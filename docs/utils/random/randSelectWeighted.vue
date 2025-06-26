<script setup lang="ts">
import { ref, computed } from "vue";
import { randSelectWeighted } from "buzzts";

const itemsText = ref<string>("a,b,c");
const weightsText = ref<string>("1,3,6");
const selected = ref<any>(null);

function generateSelected() {
  const items = itemsText.value.split(",").map(s => s.trim());
  const weights = weightsText.value.split(",").map(s => Number(s.trim()));
  if (items.length !== weights.length) {
    selected.value = "错误：选项和权重数量不匹配";
    return;
  }
  selected.value = randSelectWeighted(items, weights);
}

const selectedText = computed(() => {
  if (selected.value === null) return "点击根据权重随机选择";
  return `randSelectWeighted([${itemsText.value}] , [${weightsText.value}]) = ${selected.value}`;
});
</script>

<template>
  <n-card title="加权随机选择">
    <n-space vertical>
      <n-input v-model:value="itemsText" label="选项数组 (逗号分隔)" />
      <n-input v-model:value="weightsText" label="权重数组 (逗号分隔)" />

      <n-button type="primary" @click="generateSelected">随机选择</n-button>

      <n-gradient-text type="info">{{ selectedText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
