<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isChines } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "纯中文", value: "测试" },
  { label: "纯英文", value: "hello" },
  { label: "中英混合", value: "测试test" },
  { label: "数字", value: "12345" },
  { label: "特殊符号", value: "@#$%" },
  { label: "空字符串", value: "" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkChines() {
  result.value = isChines(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkChines();
}

watch(val, () => {
  checkChines();
});

onMounted(() => {
  checkChines();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isChines(${val.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="是否是中文校验 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入自定义字符串" />

      <n-button type="primary" @click="checkChines">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
