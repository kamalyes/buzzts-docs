<script setup lang="ts">
import { ref, computed } from "vue";
import { randUUIDv4 } from "buzzts";

const uuid = ref<string>("");

function generateUUIDv4() {
  uuid.value = randUUIDv4();
}

const uuidText = computed(() => {
  if (!uuid.value) return "点击生成UUID v4";
  return `randUUIDv4() = ${uuid.value}`;
});
</script>

<template>
  <n-card title="随机UUID v4生成">
    <n-space vertical>
      <n-button type="primary" @click="generateUUIDv4">生成UUID v4</n-button>
      <n-gradient-text type="info">{{ uuidText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
