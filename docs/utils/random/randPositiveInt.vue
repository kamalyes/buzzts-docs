<script setup lang="ts">
import { computed, ref } from "vue";
import { randPositiveInt } from "buzzts";

const intMin = ref(1);
const intMax = ref(10);
const intResult = ref<number | null>(null);
const errorMsg = ref("");

function generateInt() {
  try {
    intResult.value = randPositiveInt(intMin.value, intMax.value);
    errorMsg.value = "";
  } catch (e) {
    errorMsg.value = e instanceof Error ? e.message : "参数必须是正数";
  }
}

const intText = computed(() => {
  if (intResult.value === null) return "点击生成";
  return `randPositiveInt(${intMin.value}, ${intMax.value}) = ${intResult.value}`;
});
</script>

<template>
  <n-card title="随机正整数生成">
    <n-space vertical>
      <n-space>
        <n-input-number 
          v-model:value="intMin" 
          :min="1"
          :max="intMax - 1"
          placeholder="最小正整数"
        />
        <n-text>最小值 (≥1)</n-text>
      </n-space>
      
      <n-space>
        <n-input-number 
          v-model:value="intMax" 
          :min="intMin + 1"
          placeholder="最大正整数"
        />
        <n-text>最大值 (>min)</n-text>
      </n-space>
      
      <n-button type="primary" @click="generateInt">生成</n-button>
      
      <n-alert v-if="errorMsg" type="error">
        {{ errorMsg }}
      </n-alert>
      
      <n-gradient-text type="info">
        {{ intText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
