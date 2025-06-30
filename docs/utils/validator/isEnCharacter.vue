<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isEnCharacter } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "纯英文小写", value: "abcdef" },
  { label: "纯英文大写", value: "ABCDEF" },
  { label: "混合大小写英文", value: "AbCdEf" },
  { label: "数字混合", value: "abc123" },
  { label: "含空格", value: "abc def" },
  { label: "含特殊字符", value: "abc-def" },
  { label: "空字符串", value: "" },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

// 校验函数
function checkIsEnCharacter() {
  result.value = isEnCharacter(val.value);
}

// 点击示例按钮
function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsEnCharacter();
}

// 监听输入框变化自动校验
watch(val, () => {
  checkIsEnCharacter();
});

// 页面加载时自动校验默认示例
onMounted(() => {
  checkIsEnCharacter();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isEnCharacter("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="校验字符串是否全部为英文字符">
    <n-space vertical size="large">
      <n-space wrap>
        <!-- 多示例按钮 -->
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

      <!-- 输入框 -->
      <n-input v-model:value="val" placeholder="请输入字符串" />

      <!-- 手动校验按钮 -->
      <n-button type="primary" @click="checkIsEnCharacter">校验</n-button>

      <!-- 结果显示 -->
      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
