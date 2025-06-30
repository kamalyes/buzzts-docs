<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isHex } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "纯小写十六进制", value: "1a2b3c" },
  { label: "纯大写十六进制", value: "ABCDEF" },
  { label: "混合大小写十六进制", value: "1A2b3C" },
  { label: "非十六进制字符", value: "1g2h3i" },
  { label: "空字符串", value: "" },
  { label: "数字字符串", value: "123456" },
  { label: "带空格", value: "1a 2b" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkHex() {
  result.value = isHex(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkHex();
}

watch(val, () => {
  checkHex();
});

onMounted(() => {
  checkHex();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isHex(${val.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="是否为十六进制字符串校验 - 多示例演示">
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

      <n-button type="primary" @click="checkHex">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
