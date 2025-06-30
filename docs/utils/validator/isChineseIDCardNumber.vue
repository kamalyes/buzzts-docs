<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isChineseIDCardNumber, randString, randInt, RandType } from "buzzts";

type DemoItem = { label: string; value: string; type?: number };

const demos: DemoItem[] = [
  { label: "15位身份证（合法）", value: "130503670401001" },
  { label: "18位身份证（合法）", value: "11010519491231002X" },
  { label: "15位身份证（非法）", value: "130503670401000" },
  { label: "18位身份证（非法）", value: "110105194912310021" },
  { label: "支持15或18位（合法）", value: "11010519491231002X" },
  { label: "支持15或18位（非法）", value: "11010519491231002A" },
  { label: "18位身份证（小写x校验位）", value: "11010519491231002x" },
  { label: "18位身份证（错误长度）", value: "11010519491231002" },
  { label: "空字符串", value: "" },
  { label: "随机大写字母", value: randString(randInt(15,18), RandType.CAPITAL) },
  { label: "随机大写字母+数字", value: randString(randInt(15,18), RandType.CAPITAL| RandType.NUMBER) },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkisChineseIDCardNumber() {
  result.value = isChineseIDCardNumber(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkisChineseIDCardNumber();
}

watch([val], () => {
  checkisChineseIDCardNumber();
});

onMounted(() => {
  checkisChineseIDCardNumber();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入身份证号或选择示例"
    : `isChineseIDCardNumber("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="身份证号校验 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入身份证号" />
      <n-button type="primary" @click="checkisChineseIDCardNumber">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入身份证号或选择示例</n-text>
    </n-space>
  </n-card>
</template>
