<template>
  <form ref="form">
    <input name="username" placeholder="Username" />
    <input name="password" type="password" placeholder="Password" />
    <n-button type="button" @click="setValues">Set Values</n-button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { setFormElementValues } from 'buzzts';

// 创建对表单元素的引用
const form = ref<HTMLFormElement | null>(null);

// 定义设置表单值的函数
const setValues = () => {
  if (form.value) {
    setFormElementValues(form.value, { username: 'admin', password: '123' });
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
