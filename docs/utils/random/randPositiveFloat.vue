<script setup lang="ts">
import { computed, ref } from "vue";
import { randPositiveFloat } from "buzzts";

const floatMin = ref(0.1);
const floatMax = ref(1.0);
const precision = ref(4);
const floatResult = ref<number | null>(null);
const errorMsg = ref("");

function generateFloat() {
  try {
    floatResult.value = randPositiveFloat(floatMin.value, floatMax.value, precision.value);
    errorMsg.value = "";
  } catch (e) {
    errorMsg.value = e instanceof Error ? e.message : "参数必须是正数";
  }
}

const resultText = computed(() => {
  if (!floatResult.value) return "点击生成";
  return `randPositiveFloat(${floatMin.value}, ${floatMax.value}, ${precision.value}) = ${floatResult.value.toFixed(precision.value)}`;
});
</script>

<template>
  <n-card title="随机正浮点数生成">
    <n-space vertical>
      <n-space>
        <n-input-number 
          v-model:value="floatMin" 
          :min="0.0000000001"
          :max="floatMax - 0.0000000001"
          :step="0.1"
          placeholder="最小正数"
        />
        <n-text>最小值 (>0)</n-text>
      </n-space>
      
      <n-space>
        <n-input-number 
          v-model:value="floatMax" 
          :min="floatMin + 0.0000000001"
          :step="0.1"
          placeholder="最大正数"
        />
        <n-text>最大值 (>min)</n-text>
      </n-space>
      
      <n-space>
        <n-input-number 
          v-model:value="precision" 
          :min="1" 
          :max="16" 
          :step="1" 
          placeholder="小数位数"
        />
        <n-text>小数位数 (1-16)</n-text>
      </n-space>
      
      <n-button type="primary" @click="generateFloat">生成</n-button>
      
      <n-alert v-if="errorMsg" type="error">
        {{ errorMsg }}
      </n-alert>
      
      <n-gradient-text type="info">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
