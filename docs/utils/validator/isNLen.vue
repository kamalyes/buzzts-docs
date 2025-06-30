<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isNLen } from "buzzts";

type DemoItem = { label: string; value: string; n: number };

const demos: DemoItem[] = [
  { label: "长度4，任意字符", value: "abcd", n: 4 },
  { label: "长度3，任意字符", value: "123", n: 3 },
  { label: "长度5，含特殊字符", value: "!@#$%", n: 5 },
  { label: "长度2，空格", value: "  ", n: 2 },
  { label: "长度1，单字符", value: "x", n: 1 },
  { label: "长度4，少于指定长度", value: "abc", n: 4 },
  { label: "长度4，多于指定长度", value: "abcde", n: 4 },
  { label: "空字符串，长度0", value: "", n: 0 },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref(demos[0].value);
const n = ref(demos[0].n);
const result = ref<boolean | null>(null);

// 校验函数
function checkIsNLen() {
  result.value = isNLen(val.value, n.value);
}

// 点击示例按钮
function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  n.value = demos[index].n;
  checkIsNLen();
}

// 监听输入框和长度变化自动校验
watch([val, n], () => {
  checkIsNLen();
});

// 页面加载时自动校验默认示例
onMounted(() => {
  checkIsNLen();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串和长度或选择示例"
    : `isNLen("${val.value}", ${n.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="校验字符串是否为指定长度">
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

      <!-- 长度输入框 -->
      <n-input-number v-model:value="n" :min="0" placeholder="请输入长度" style="width: 120px;" />

      <!-- 手动校验按钮 -->
      <n-button type="primary" @click="checkIsNLen">校验</n-button>

      <!-- 结果显示 -->
      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串和长度或选择示例</n-text>
    </n-space>
  </n-card>
</template>
