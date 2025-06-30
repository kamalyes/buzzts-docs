<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(3)

import localStorage from "./localStorage.vue"
import sessionStorage from "./sessionStorage.vue"
import cookies from "./cookies.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
Storage 操作工具集
:::

### localStorage

localStorage 操作演示组件，支持增删改查和清空。

<div class="buzzts-border">

#### <divider-base /> {#base-localStorage}

<localStorage />

<details>
<summary>查看代码</summary>

<<< @/utils/storage/localStorage.vue

</details>

#### <divider-param /> {#param-localStorage}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| key      | 存储的键名 | string | 无     |
| value    | 存储的值   | string | 无     |

| 返回值 | 说明       |
|--------|------------|
| void   | 操作后通过界面显示结果 |

#### <divider-desc /> {#desc-localStorage}

- 使用 StorageWrapper 封装 localStorage。
- 支持自动序列化和反序列化。
- 提供增删改查和清空操作。

</div>

---

### sessionStorage

sessionStorage 操作演示组件，支持增删改查和清空。

<div class="buzzts-border">

#### <divider-base /> {#base-sessionStorage}

<sessionStorage />

<details>
<summary>查看代码</summary>

<<< @/utils/storage/sessionStorage.vue

</details>

#### <divider-param /> {#param-sessionStorage}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| key      | 存储的键名 | string | 无     |
| value    | 存储的值   | string | 无     |

| 返回值 | 说明       |
|--------|------------|
| void   | 操作后通过界面显示结果 |

#### <divider-desc /> {#desc-sessionStorage}

- 使用 StorageWrapper 封装 sessionStorage。
- 支持自动序列化和反序列化。
- 提供增删改查和清空操作。

</div>

---

### cookies

Cookie 操作演示组件，支持增删改查和清空。

<div class="buzzts-border">

#### <divider-base /> {#base-cookies}

<cookies />

<details>
<summary>查看代码</summary>

<<< @/utils/storage/cookies.vue

</details>

#### <divider-param /> {#param-cookies}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| key      | 存储的键名 | string | 无     |
| value    | 存储的值   | string | 无     |

| 返回值 | 说明       |
|--------|------------|
| void   | 操作后通过界面显示结果 |

#### <divider-desc /> {#desc-cookies}

- 使用 CookieWrapper 封装 Cookie 操作。
- 设置时支持 expires 和 path 选项（默认 1 天有效期，路径 /）。
- 提供增删改查和清空操作。

</div>
