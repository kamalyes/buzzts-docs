<script setup lang="ts">
import { ref, computed, watch } from 'vue';
import { isNumberWithRules, NumberCheckOptions } from 'buzzts';

type DemoItem = {
  label: string;
  value: string;
  options: NumberCheckOptions;
  description?: string;
};

const demos: DemoItem[] = [
  { label: "纯整数正数", value: "123", options: { allowDecimal: false }, description: "允许正负号，整数最小长度1" },
  { label: "纯整数负数", value: "-786", options: { allowDecimal: false }, description: "带负号的整数" },
  { label: "整数0开头禁止", value: "0123", options: { allowDecimal: false, nonZeroStart: true }, description: "整数不能以0开头" },
  { label: "整数0开头允许", value: "0123", options: { allowDecimal: false, nonZeroStart: false }, description: "整数允许以0开头" },
  { label: "纯小数无整数部分允许", value: ".58", options: { allowDecimal: true, allowNoIntegerPart: true, minDecimalLength: 1, maxDecimalLength: 2 }, description: "无整数部分的小数" },
  { label: "纯小数无整数部分禁止", value: ".58", options: { allowDecimal: true, allowNoIntegerPart: false, minDecimalLength: 1, maxDecimalLength: 2 }, description: "禁止无整数部分小数" },
  { label: "小数整数和小数部分", value: "123.78", options: { allowDecimal: true, minDecimalLength: 1, maxDecimalLength: 2 }, description: "整数+小数" },
  { label: "小数最小长度不满足", value: "123.58", options: { allowDecimal: true, minDecimalLength: 2, maxDecimalLength: 2 }, description: "小数位数少于最小" },
  { label: "小数最大长度超出", value: "123.786", options: { allowDecimal: true, minDecimalLength: 1, maxDecimalLength: 2 }, description: "小数位数超过最大" },
  { label: "禁止正号", value: "+123", options: { allowDecimal: false, allowPositiveSign: false }, description: "禁止使用正号" },
  { label: "允许正号", value: "+123", options: { allowDecimal: false, allowPositiveSign: true }, description: "允许使用正号" },
  { label: "禁止负号", value: "-123", options: { allowDecimal: false, allowNegativeSign: false }, description: "禁止负号" },
  { label: "允许负号", value: "-123", options: { allowDecimal: false, allowNegativeSign: true }, description: "允许负号" },
  { label: "整数长度限制", value: "12378", options: { allowDecimal: false, minIntegerLength: 3, maxIntegerLength: 5 }, description: "整数长度3-5" },
  { label: "整数长度超长", value: "123786", options: { allowDecimal: false, minIntegerLength: 3, maxIntegerLength: 5 }, description: "整数长度超出最大" },
  { label: "整数长度不足", value: "12", options: { allowDecimal: false, minIntegerLength: 3, maxIntegerLength: 5 }, description: "整数长度小于最小" },
  { label: "小数长度限制", value: "123.7867", options: { allowDecimal: true, minDecimalLength: 2, maxDecimalLength: 4 }, description: "小数长度2-4" },
  { label: "小数长度不足", value: "123.58", options: { allowDecimal: true, minDecimalLength: 2, maxDecimalLength: 4 }, description: "小数长度少于最小" },
  { label: "小数长度超长", value: "123.78678", options: { allowDecimal: true, minDecimalLength: 2, maxDecimalLength: 4 }, description: "小数长度超过最大" },
  { label: "只允许整数", value: "123.78", options: { allowDecimal: false }, description: "禁止小数，输入小数" },
  { label: "允许无符号", value: "123", options: { allowPositiveSign: false, allowNegativeSign: false, allowDecimal: false }, description: "不允许符号" },
  { label: "空字符串", value: "", options: { allowDecimal: true }, description: "空字符串不通过" },
];

const val = ref('');
const options = ref<NumberCheckOptions>({
  allowPositiveSign: true,
  allowNegativeSign: true,
  minIntegerLength: 1,
  allowDecimal: false,
  minDecimalLength: 0,
  maxDecimalLength: 0,
  allowNoIntegerPart: false,
  nonZeroStart: true,
});

const selectedIndex = ref(-1);
const result = ref<boolean | null>(null);

function selectDemo(index: number) {
  selectedIndex.value = index;
  const demo = demos[index];
  val.value = demo.value;
  options.value = { ...demo.options };
}

function checkNumber() {
  if (val.value.trim() === '') {
    result.value = null;
    return;
  }
  try {
    result.value = isNumberWithRules(val.value.trim(), options.value);
  } catch {
    result.value = false;
  }
}

watch([val, options], () => {
  checkNumber();
}, { immediate: true });

const resultText = computed(() => {
  if (result.value === null) return '请输入数字字符串或选择测试示例';
  return `isNumberWithRules("${val.value}", ${JSON.stringify(options.value)}) = ${result.value}`;
});
</script>

<template>
  <n-card title="数字字符串校验 - 全面测试示例" style="max-width: 700px; margin: 20px auto;">
    <n-space vertical size="large" style="width: 100%;">
      <!-- 示例按钮 -->
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
          :title="item.description"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <!-- 输入框 -->
      <n-input
        v-model:value="val"
        placeholder="请输入数字字符串"
        clearable
      />

      <!-- 选项复选框 -->
      <n-space wrap>
        <n-checkbox v-model:value="options.allowPositiveSign">允许正号</n-checkbox>
        <n-checkbox v-model:value="options.allowNegativeSign">允许负号</n-checkbox>
        <n-checkbox v-model:value="options.allowDecimal">允许小数</n-checkbox>
        <n-checkbox v-model:value="options.allowNoIntegerPart" :disabled="!options.allowDecimal">允许无整数部分</n-checkbox>
        <n-checkbox v-model:value="options.nonZeroStart">整数非零开头</n-checkbox>
      </n-space>

      <!-- 整数长度 -->
      <n-space align="center" size="small" style="flex-wrap: wrap;">
        <label>整数最小长度：</label>
        <n-input-number
          v-model:value="options.minIntegerLength"
          :min="0"
          :max="options.maxIntegerLength || undefined"
          style="width: 100px;"
          :disabled="false"
        />
        <label style="margin-left: 1rem;">整数最大长度：</label>
        <n-input-number
          v-model:value="options.maxIntegerLength"
          :min="0"
          placeholder="不限"
          style="width: 100px;"
        />
      </n-space>

      <!-- 小数长度 -->
      <n-space align="center" size="small" style="flex-wrap: wrap;">
        <label>小数最小长度：</label>
        <n-input-number
          v-model:value="options.minDecimalLength"
          :min="0"
          style="width: 100px;"
          :disabled="!options.allowDecimal"
        />
        <label style="margin-left: 1rem;">小数最大长度：</label>
        <n-input-number
          v-model:value="options.maxDecimalLength"
          :min="0"
          placeholder="0"
          style="width: 100px;"
          :disabled="!options.allowDecimal"
        />
      </n-space>

      <!-- 结果显示 -->
      <n-gradient-text
        type="info"
        style="margin-top: 12px; display: block;"
      >
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
