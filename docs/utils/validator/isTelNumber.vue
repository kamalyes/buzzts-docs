<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isTelNumber } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "合法手机号", value: "13800138000" },
  { label: "非法手机号 - 数字不足11位", value: "1234567890" },
  { label: "非法手机号 - 12位多余数字", value: "138001380000" },
  { label: "非法手机号 - 前缀不对", value: "11800138000" },
  { label: "手机号带空格", value: "138 0013 8000" },
  { label: "手机号带横线", value: "138-0013-8000" },
  { label: "手机号带国码", value: "+8613800138000" },
  { label: "空字符串", value: "" },
  { label: "随机字符串", value: "abc123" },
  { label: "全是0", value: "00000000000" },
  { label: "手机号带括号", value: "(138)00138000" },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsTelNumber() {
  result.value = isTelNumber(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsTelNumber();
}

watch(val, () => {
  checkIsTelNumber();
});

onMounted(() => {
  checkIsTelNumber();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入手机号或选择示例"
    : `isTelNumber("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="手机号校验 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入手机号" />

      <n-button type="primary" @click="checkIsTelNumber">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入手机号或选择示例</n-text>
    </n-space>
  </n-card>
</template>
