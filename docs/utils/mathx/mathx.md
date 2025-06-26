<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(4)

import arrayAllExist from "./arrayAllExist.vue"
import arrayAllExistDeep from "./arrayAllExistDeep.vue"
import arrayAnyExist from "./arrayAnyExist.vue"
import arrayAnyExistDeep from "./arrayAnyExistDeep.vue"
</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理数组
:::

## arrayAllExist

检测一个数组是否包含另一个数组中所有的值（内部使用`new Set`性能更好。该方法只针对基本数据类型，需要更复杂的场景可以用`arrayAllExistDeep`）

<div class="buzzts-border">

#### <divider-base /> {#base3}

<arrayAllExist />

<details>

<summary>查看代码</summary>

<<< @/utils/mathx/arrayAllExist.vue

</details>

#### <divider-param /> {#param3}

接收二个参数，第一个参数 `array`，第二个参数 `checkArray`，返回值类型为 `boolean`

| **参数属性** | **说明**               | **类型**         |
| ------------ | ---------------------- | ---------------- |
| `array`      | 初始数组               | `Array<unknown>` |
| `checkArray` | 与初始数组做对比的数组 | `Array<unknown>` |

</div>

## arrayAllExistDeep

检测一个数组是否包含另一个数组中所有的值（深度对比）

<div class="buzzts-border">

#### <divider-base /> {#base4}

<arrayAllExistDeep />

<details>

<summary>查看代码</summary>

<<< @/utils/mathx/arrayAllExistDeep.vue

</details>

#### <divider-param /> {#param4}

接收二个参数，第一个参数 `array`，第二个参数 `checkArray`，返回值类型为 `boolean`

| **参数属性** | **说明**               | **类型**         |
| ------------ | ---------------------- | ---------------- |
| `array`      | 初始数组               | `Array<unknown>` |
| `checkArray` | 与初始数组做对比的数组 | `Array<unknown>` |

</div>

## arrayAnyExist

检测一个数组是否包含另一个数组中任意一个值（内部使用`new Set`性能更好。该方法只针对基本数据类型，需要更复杂的场景可以用`arrayAnyExistDeep`）

<div class="buzzts-border">

#### <divider-base /> {#base5}

<arrayAnyExist />

<details>

<summary>查看代码</summary>

<<< @/utils/mathx/arrayAnyExist.vue

</details>

#### <divider-param /> {#param5}

接收二个参数，第一个参数 `array`，第二个参数 `checkArray`，返回值类型为 `boolean`

| **参数属性** | **说明**               | **类型**         |
| ------------ | ---------------------- | ---------------- |
| `array`      | 初始数组               | `Array<unknown>` |
| `checkArray` | 与初始数组做对比的数组 | `Array<unknown>` |

</div>

## arrayAnyExistDeep

检测一个数组是否包含另一个数组中任意一个值（深度对比）

<div class="buzzts-border">

#### <divider-base /> {#base6}

<arrayAnyExistDeep />

<details>

<summary>查看代码</summary>

<<< @/utils/mathx/arrayAnyExistDeep.vue

</details>

#### <divider-param /> {#param6}

接收二个参数，第一个参数 `array`，第二个参数 `checkArray`，返回值类型为 `boolean`

| **参数属性** | **说明**               | **类型**         |
| ------------ | ---------------------- | ---------------- |
| `array`      | 初始数组               | `Array<unknown>` |
| `checkArray` | 与初始数组做对比的数组 | `Array<unknown>` |

</div>