<script setup lang="ts">
import { ref, computed } from 'vue';
import { getImageFileName } from 'buzzts';

const fileName = ref<string | null>(null);

function generateImageFileName() {
  fileName.value = getImageFileName();
}

const resultText = computed(() => {
  return  `getImageFileName()= ${JSON.stringify(fileName.value)}\n`;
});
</script>

<template>
  <n-card title="生成文件名">
    <n-space vertical size="large">
      <n-button type="primary" @click="generateImageFileName">生成文件名</n-button>
      <n-gradient-text v-if="fileName !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
