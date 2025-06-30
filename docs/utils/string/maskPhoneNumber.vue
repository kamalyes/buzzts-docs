<script setup lang="ts">
import { ref, computed, watch } from "vue";
import { maskPhoneNumber, randString, RandType } from "buzzts";

const phoneNumber = ref<string>(`138${randString(8, RandType.NUMBER)}`); // 默认示例手机号
const maskChar = ref<string>("*");             // 默认替换字符
const maskLength = ref<number>(4);              // 默认替换长度

const result = ref<string>("");

// 监听手机号输入，自动清空结果，避免误导
watch(phoneNumber, () => {
  result.value = "";
});

function generateMaskedPhone() {
  // 简单校验手机号长度
  if (phoneNumber.value.length !== 11 || !/^\d{11}$/.test(phoneNumber.value)) {
    result.value = "请输入有效的11位手机号";
    return;
  }
  result.value = maskPhoneNumber(phoneNumber.value, {
    maskChar: maskChar.value,
    maskLength: maskLength.value,
  });
}

const resultText = computed(() => {
  if (!result.value) return "请输入手机号后点击加密";
  return `maskPhoneNumber(${phoneNumber.value}, {
    maskChar: ${maskChar.value},
    maskLength: ${maskLength.value}
  }) = ${result.value}`;
});
</script>

<template>
  <n-card title="手机号加密">
    <n-space vertical>
      <n-input
        v-model:value="phoneNumber"
        label="手机号"
        placeholder="请输入11位手机号"
        maxlength="11"
        clearable
      />
      <n-text>手机号</n-text>

      <n-input
        v-model:value="maskChar"
        label="替换字符"
        maxlength="1"
        placeholder="默认 *"
      />
      <n-text>替换字符</n-text>

      <n-input-number
        v-model:value="maskLength"
        label="替换长度"
        :min="1"
        :max="11"
      />
      <n-text>替换长度</n-text>

      <n-button type="primary" @click="generateMaskedPhone">加密</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
