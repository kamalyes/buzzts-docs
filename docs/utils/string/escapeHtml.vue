<script setup lang="ts">
import { ref, computed } from "vue";
import { escapeHtml } from "buzzts";

const input = ref<string>('<div class="test">Hello & Welcome!</div>'); 
const result = ref<string>("");

function generateEscaped() {
  result.value = escapeHtml(input.value);
}

const resultText = computed(() => {
  if (!result.value) return "请输入HTML字符串后点击转义";
  return `escapeHtml() = ${result.value}`;
});
</script>

<template>
  <n-card title="HTML特殊字符转义">
    <n-space vertical>
      <n-input v-model:value="input" label="HTML字符串" type="textarea" />

      <n-button type="primary" @click="generateEscaped">转义</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
