<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { getPercentage } from "buzzts";

type DemoItem = { label: string; part: number; total: number; decimalPlaces?: number };

const demos: DemoItem[] = [
  { label: "1 / 2，保留2位", part: 1, total: 2, decimalPlaces: 2 },
  { label: "1 / 3，默认保留2位", part: 1, total: 3 },
  { label: "0 / 0，返回0%", part: 0, total: 0 },
  { label: "50 / 200，保留1位", part: 50, total: 200, decimalPlaces: 1 },
  { label: "非数字参数（测试异常）", part: NaN, total: 10 },
];

const selectedIndex = ref(0);
const part = ref(demos[0].part);
const total = ref(demos[0].total);
const decimalPlaces = ref(demos[0].decimalPlaces ?? 2);
const result = ref<string | null>(null);
const errorMsg = ref<string>("");

function tryGetPercentage() {
  errorMsg.value = "";
  try {
    result.value = getPercentage(part.value, total.value, decimalPlaces.value);
  } catch (error: any) {
    result.value = null;
    errorMsg.value = error.message || "未知错误";
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  part.value = demos[index].part;
  total.value = demos[index].total;
  decimalPlaces.value = demos[index].decimalPlaces ?? 2;
  tryGetPercentage();
}

watch([part, total, decimalPlaces], () => {
  tryGetPercentage();
});

onMounted(() => {
  tryGetPercentage();
});

const resultText = computed(() => {
  if (errorMsg.value) return `错误: ${errorMsg.value}`;
  if (result.value === null) return "请输入参数";
  return `getPercentage(${part.value}, ${total.value}, ${decimalPlaces.value}) = ${result.value}`;
});
</script>

<template>
  <n-card title="getPercentage - 百分比计算演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <n-input-number v-model:value="part" placeholder="当前值" />
      <n-input-number v-model:value="total" placeholder="总值" />
      <n-input-number v-model:value="decimalPlaces" placeholder="保留小数位" :min="0" />

      <n-button type="primary" @click="tryGetPercentage">计算百分比</n-button>

      <n-text style="margin-top: 12px;" type="error" v-if="errorMsg">{{ errorMsg }}</n-text>
      <n-text style="margin-top: 12px;" v-else>{{ resultText }}</n-text>
    </n-space>
  </n-card>
</template>
