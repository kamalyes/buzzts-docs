<script setup lang="ts">
import { ref, computed } from "vue";
import { randEmail } from "buzzts";

const domain = ref<string>("example.com");
const result = ref<string>("");

function generateEmail() {
  result.value = randEmail(domain.value);
}

const resultText = computed(() => {
  if (!result.value) return "点击生成随机邮箱";
  return `randEmail() = ${result.value}`;
});
</script>

<template>
  <n-card title="随机邮箱生成">
    <n-space vertical>
      <n-input v-model:value="domain" label="邮箱域名" />

      <n-button type="primary" @click="generateEmail">生成邮箱</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>