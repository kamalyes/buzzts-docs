<script setup lang="ts">
import { useData } from "vitepress";
import { darkTheme } from "naive-ui";
import { ref, watch, onMounted, computed } from "vue";
import hljs from "highlight.js/lib/core";
import javascript from "highlight.js/lib/languages/javascript";

// Register highlight.js language
hljs.registerLanguage("javascript", javascript);

const show = ref(false);
const dark = ref(false);
const { isDark, page } = useData();

onMounted(() => {
  const time = page.value.title === "useECharts" ? 500 : 60;
  dark.value = isDark.value;
  setTimeout(() => {
    show.value = true;
  }, time);
});

watch(
  () => isDark.value,
  (val) => {
    dark.value = val;
  }
);
</script>

<template>
  <n-config-provider
    v-show="show"
    :theme="dark ? darkTheme : undefined"
    :hljs="hljs"
  >
    <slot :dark="dark" />
  </n-config-provider>
</template>
