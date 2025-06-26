<script setup lang="ts">
import { ref, computed } from "vue";
import { randUUIDv1 } from "buzzts";

const uuid = ref<string>("");

function generateUUIDv1() {
  uuid.value = randUUIDv1();
}

const uuidText = computed(() => {
  if (!uuid.value) return "点击生成UUID v1";
  return `randUUIDv1() = ${uuid.value}`;
});
</script>

<template>
  <n-card title="随机UUID v1生成">
    <n-space vertical>
      <n-button type="primary" @click="generateUUIDv1">生成UUID v1</n-button>
      <n-gradient-text type="info">{{ uuidText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
