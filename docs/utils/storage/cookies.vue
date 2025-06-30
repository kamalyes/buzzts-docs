<script setup lang="ts">
import { ref, watch, computed, onMounted } from "vue";
import { CookieWrapper } from "buzzts";

const cookieWrapper = new CookieWrapper();

type DemoItem = { label: string; key: string; value: string; options?: Record<string, any> };

const demos: DemoItem[] = [
  { label: "简单设置读取示例1", key: "cookieKey1", value: "cookieValue1" },
  { label: "简单设置读取示例2", key: "cookieKey2", value: "cookieValue2" },
  { label: "设置15分钟过期", key: "cookieKey3", value: "expiresIn1m", options: { expires: 1/96, path: "/" } },
  { label: "设置带Secure和SameSite", key: "cookieKey4", value: "secureSameSite", options: { expires: 7, path: "/", secure: true, sameSite: "Strict" } },
  { label: "设置自定义路径", key: "cookieKey5", value: "customPath", options: { expires: 3, path: "/test" } },
];

const selectedIndex = ref(0);
const key = ref(demos[0].key);
const val = ref(demos[0].value);
const options = ref<Record<string, any>>(demos[0].options || {});

const lastCall = ref<{ func: string; args: any[] } | null>(null);
const result = ref("");

function setItem() {
  try {
    lastCall.value = { func: "set", args: [key.value, val.value, options.value] };
    cookieWrapper.set(key.value, val.value, options.value);
    result.value = `Cookie 设置成功`;
  } catch (e) {
    result.value = `设置失败: ${(e as Error).message}`;
  }
}

function getItem() {
  try {
    lastCall.value = { func: "get", args: [key.value] };
    const v = cookieWrapper.get(key.value);
    result.value = v === null ? "无对应值" : `Cookie 读取到: ${v}`;
  } catch (e) {
    result.value = `读取失败: ${(e as Error).message}`;
  }
}

function removeItem() {
  try {
    lastCall.value = { func: "remove", args: [key.value, options.value] };
    cookieWrapper.remove(key.value, options.value);
    result.value = `Cookie 删除成功`;
  } catch (e) {
    result.value = `删除失败: ${(e as Error).message}`;
  }
}

function clearStorage() {
  try {
    lastCall.value = { func: "clear", args: [] };
    cookieWrapper.clear();
    result.value = "Cookie 已清空所有数据";
  } catch (e) {
    result.value = `清空失败: ${(e as Error).message}`;
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  key.value = demos[index].key;
  val.value = demos[index].value;
  options.value = demos[index].options || {};
  lastCall.value = null;
  result.value = "";
}

watch(key, () => {
  lastCall.value = null;
  result.value = "";
});

const resultText = computed(() => {
  if (!lastCall.value) return "请点击按钮执行操作";
  const { func, args } = lastCall.value;
  const argsStr = args.map((a) => JSON.stringify(a)).join(", ");
  return `cookieWrapper.${func}(${argsStr})`;
});

onMounted(() => {
  selectDemo(0);
});
</script>

<template>
  <n-card title="Cookie 操作演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <n-space>
        <n-input v-model:value="key" placeholder="请输入 key" style="width: 200px" />
        <n-input v-model:value="val" placeholder="请输入 value" style="width: 200px" />
      </n-space>

      <n-space align="center" style="flex-wrap: wrap;">
        <n-form-item label="expires (天)">
          <n-input-number
            v-model:value="options.expires"
            :min="0"
            style="width: 230px"
            placeholder="天数"
          />
        </n-form-item>

        <n-form-item label="path">
          <n-input v-model:value="options.path" placeholder="路径" style="width: 200px" />
        </n-form-item>

        <n-form-item label="secure">
          <n-switch v-model:value="options.secure" />
        </n-form-item>

        <n-form-item label="sameSite">
          <n-select
            v-model:value="options.sameSite"
            :options="[
              { label: 'Lax', value: 'Lax' },
              { label: 'Strict', value: 'Strict' },
              { label: 'None', value: 'None' }
            ]"
            placeholder="SameSite"
            style="width: 120px"
            clearable
          />
        </n-form-item>
      </n-space>

      <n-space>
        <n-button type="success" @click="setItem">设置</n-button>
        <n-button type="info" @click="getItem">读取</n-button>
        <n-button type="warning" @click="removeItem">删除</n-button>
        <n-button type="error" @click="clearStorage">清空全部</n-button>
      </n-space>
      <n-gradient-text type="info" v-if="resultText"> {{ resultText }} </n-gradient-text>
      <n-text style="white-space: pre-wrap; margin-top: 6px;" v-if="result">{{ result }}</n-text>
    </n-space>
  </n-card>
</template>
