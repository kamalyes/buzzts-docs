<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(4)

import sleep from "./sleep.vue"
import timeoutPromise from "./timeoutPromise.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
限流工具集
:::

### Sleep

可取消的延迟等待类，封装了延迟 Promise 和取消功能

<div class="buzzts-border">

#### <divider-base /> {#base-sleep}

<sleep />

<details>
<summary>查看代码</summary>

<<< @/utils/rate/sleep.vue

</details>

#### <divider-param /> {#param-sleep}

| 参数属性 | 说明                       | 类型           | 默认值 |
|----------|----------------------------|----------------|--------|
| wait     | 等待时间，单位毫秒         | `number`       | 无     |
| callback | 等待结束时调用的回调函数   | `() => void`   | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| 无       | 实例包含 `promise` 和 `cancel` 方法 |

#### <divider-desc /> {#desc-sleep}

- 封装延迟 Promise，支持异步等待  
- 支持取消等待，调用 `cancel` 会拒绝 Promise  
- 常用于异步等待场景，支持等待结束回调  

</div>

### TimeoutPromise

给 Promise 设置超时时间的包装类，超过指定时间未完成则自动拒绝

<div class="buzzts-border">

#### <divider-base /> {#base-timeoutPromise}

<timeoutPromise />

<details>
<summary>查看代码</summary>

<<< @/utils/rate/timeoutPromise.vue

</details>

#### <divider-param /> {#param-timeoutPromise}

| 参数属性 | 说明              | 类型           | 默认值 |
|----------|-------------------|----------------|--------|
| promise  | 需要设置超时的 Promise | `Promise<T>`  | 无     |
| ms       | 超时时间，单位毫秒 | `number`       | 无     |

| 返回值   | 说明                      |
|----------|---------------------------|
| `Promise<T>` | 带超时限制的 Promise    |

#### <divider-desc /> {#desc-timeoutPromise}

- 包装 Promise，添加超时功能  
- 超过指定时间未完成，自动拒绝并抛出超时错误  
- 常用于网络请求等异步操作的超时控制  

</div>
