
<script setup lang="ts">
import { ref, computed } from "vue";
import { unescapeHtml, randInt, randString, RandType } from "buzzts";

const input = ref<string>('');

function generateInput() {
  const randomSuffix = randString(randInt(5, 20), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER);
  input.value = `&lt;div class=&quot;test&quot;&gt;Hello &amp; ${randomSuffix} Welcome!&lt;&#x2F;div&gt;`;
}
generateInput();

const result = ref<string>('');

function handleUnescape() {
  result.value = unescapeHtml(input.value);
}

const resultText = computed(() => {
  if (!result.value) return "请输入转义后的字符串";
  return `unescapeHtml() = ${result.value}`;
});
</script>

<template>
  <n-card title="HTML实体反转义">
    <n-space vertical>
      <n-input v-model:value="input" label="转义字符串" placeholder="例如 &amp;lt;div&amp;gt;" />

      <n-button type="primary" @click="handleUnescape">反转义</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
