<template>
  <form ref="form" @submit.prevent="serialize">
    <input name="username" v-model="username" placeholder="Username" />
    <input name="password" v-model="password" type="password" placeholder="Password" />
    <n-button type="submit">Submit</n-button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { serializeFormElement } from 'buzzts';

// 定义响应式变量
const form = ref<HTMLFormElement | null>(null);
const username = ref('');
const password = ref('');

// 定义序列化函数
const serialize = () => {
  if (form.value) {
    const data = serializeFormElement(form.value);
    console.log(data); // 打印序列化后的数据
  }
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
