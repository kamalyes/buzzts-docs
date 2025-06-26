<script setup lang="ts">
import { ref, computed } from "vue";
import { randCirclePointInside } from "buzzts";

const radius = ref<number>(10);
const point = ref<{ x: number; y: number } | null>(null);

function generatePoint() {
  if (radius.value < 0) {
    point.value = null;
    return;
  }
  point.value = randCirclePointInside(radius.value);
}

const pointText = computed(() => {
  if (!point.value) return "点击生成圆内随机点";
  return `randCirclePointInside() = { x: ${point.value.x.toFixed(2)}, y: ${point.value.y.toFixed(2)} }`;
});
</script>

<template>
  <n-card title="圆内随机点生成">
    <n-space vertical>
      <n-input-number v-model:value="radius" :min="0" label="圆半径" />

      <n-button type="primary" @click="generatePoint">生成点</n-button>

      <n-gradient-text type="info">{{ pointText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
