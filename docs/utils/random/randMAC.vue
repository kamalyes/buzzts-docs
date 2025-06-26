<script setup lang="ts">
import { ref } from "vue";
import { randMAC } from "buzzts";

const result = ref<string>("");

function generateMAC() {
  result.value = randMAC();
}
</script>

<template>
  <n-card title="随机MAC地址生成">
    <n-space vertical>
      <n-button type="primary" @click="generateMAC">生成MAC地址</n-button>
      <n-gradient-text type="info">{{ result }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
