<template>
  <n-card title="人民币格式化器">
    <n-space vertical>
      <n-input-number v-model:value="amount" placeholder="输入金额" clearable />
      <n-input-number v-model:value="precision" placeholder="输入精度" clearable />
      <n-select 
        v-model:value="unit" 
        placeholder="选择单位" 
        :options="unitOptions"
        clearable>
      </n-select>
      <n-gradient-text type="info">当前金额（元）: {{ formattedAmount.toYuan() }}</n-gradient-text>
      <n-gradient-text type="info">当前金额（角）: {{ formattedAmount.toJiao() }}</n-gradient-text>
      <n-gradient-text type="info">当前金额（分）: {{ formattedAmount.toCents() }}</n-gradient-text>
      <n-gradient-text type="info">当前金额（厘）: {{ formattedAmount.toLi() }}</n-gradient-text>
      <n-gradient-text type="info">当前精度: {{ formattedAmount.precision }}</n-gradient-text>
    </n-space>
  </n-card>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { RmbFormatter } from 'buzzts'; // 假设导入路径

const rmbFormatter = new RmbFormatter();
const amount = ref(1);
const unit = ref<'yuan' | 'jiao' | 'cents' | 'li'>('yuan');
const precision = ref(2);

// 单位选项数组
const unitOptions = [
  { label: '元', value: 'yuan' },
  { label: '角', value: 'jiao' },
  { label: '分', value: 'cents' },
  { label: '厘', value: 'li' }
];

// 计算属性，用于动态获取格式化后的金额
const formattedAmount = computed(() => {
  rmbFormatter.setAmount(amount.value, unit.value);
  rmbFormatter.setPrecision(precision.value);
  return rmbFormatter;
});

</script>

<style scoped>
/* 在这里添加样式 */
</style>
