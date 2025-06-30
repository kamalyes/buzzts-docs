<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { chunkArray } from "buzzts";

type DemoItem = { label: string; value: number[]; chunkCount: number };

const demos: DemoItem[] = [
  { label: "10个数字分2块", value: [1,2,3,4,5,6,7,8,9,10], chunkCount: 2 },
  { label: "10个数字分3块", value: [1,2,3,4,5,6,7,8,9,10], chunkCount: 3 },
  { label: "5个数字分10块（块数大于长度）", value: [1,2,3,4,5], chunkCount: 10 },
  { label: "空数组分1块", value: [], chunkCount: 1 },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const chunkCount = ref(demos[0].chunkCount);
const result = ref<number[][] | string | null>(null);
const errorMsg = ref<string>("");

function tryChunkArray() {
  errorMsg.value = "";
  try {
    result.value = chunkArray(val.value, chunkCount.value);
  } catch (error: any) {
    result.value = null;
    errorMsg.value = error.message || "未知错误";
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  chunkCount.value = demos[index].chunkCount;
  tryChunkArray();
}

watch([val, chunkCount], () => {
  tryChunkArray();
});

onMounted(() => {
  tryChunkArray();
});

const resultText = computed(() => {
  if (errorMsg.value) return `错误: ${errorMsg.value}`;
  if (result.value === null) return "请设置数组和分块数";
  return JSON.stringify(result.value);
});
</script>

<template>
  <n-card title="chunkArray - 数组分块演示">
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

      <n-input
        v-model:value="val"
        placeholder="请输入数组，逗号分隔"
        @change="val = val.split(',').map(v => Number(v.trim())).filter(v => !isNaN(v))"
      />

      <n-input-number
        v-model:value="chunkCount"
        placeholder="分块数"
        :min="1"
        :max="val.length"
      />

      <n-button type="primary" @click="tryChunkArray">分块</n-button>

      <n-text style="margin-top: 12px;" type="error" v-if="errorMsg">{{ errorMsg }}</n-text>
      <n-text style="margin-top: 12px;" v-else>{{ resultText }}</n-text>
    </n-space>
  </n-card>
</template>
