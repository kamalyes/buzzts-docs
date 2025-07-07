<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(17)

import arrayAllExist from "./arrayAllExist.vue"
import arrayAllExistDeep from "./arrayAllExistDeep.vue"
import arrayAnyExist from "./arrayAnyExist.vue"
import arrayAnyExistDeep from "./arrayAnyExistDeep.vue"
import getDistance from "./getDistance.vue"
import getBetween from "./getBetween.vue"
import deepClone from "./deepClone.vue"
import mergeObject from "./mergeObject.vue"
import intToLowerChinese from "./intToLowerChinese.vue"
import upperMoney from "./upperMoney.vue"
import sumAverage from "./sumAverage.vue"
import chunkArray from "./chunkArray.vue"
import getPercentage from "./getPercentage.vue"
import arrayToObject from "./arrayToObject.vue"
import extractPropertyToArray from "./extractPropertyToArray.vue"
import toMappedArray from "./toMappedArray.vue"
import findValueByKey from "./findValueByKey.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理数据工具集
:::

### extractPropertyToArray

提取给定对象数组中所有指定属性的值

<div class="buzzts-border">

#### <divider-base /> {#base-extractPropertyToArray}

<extractPropertyToArray />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/extractPropertyToArray.vue

</details>

#### <divider-param /> {#param-extractPropertyToArray}

| 参数属性 | 说明                            | 类型                            | 默认值 |
|----------|---------------------------------|---------------------------------|--------|
| items    | 对象数组，每个对象应包含可选的指定属性 | `Array<T> \| null \| undefined` | 无     |
| key      | 要提取的属性名，类型为对象的键   | `K`                             | 无     |
| excludeNil| 是否排除 null 和 undefined，默认为 false | `boolean`                       | `false`|

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Array<T[K]>` | 返回所有指定属性值的数组，如果未提供有效的 `items`，则返回空数组 |

#### <divider-desc /> {#desc-extractPropertyToArray}

- 提取对象数组中所有指定属性的值，支持可选地排除 null 和 undefined 的项
</div>

### arrayToObject

将字符串数组转换为对象数组，每个对象包含指定的属性，对应数组中的字符串可选地，排除值为 null 的项。

<div class="buzzts-border">

#### <divider-base /> {#base-arrayToObject}

<arrayToObject />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/arrayToObject.vue

</details>

#### <divider-param /> {#param-arrayToObject}

| 参数属性 | 说明                             | 类型                            | 默认值 |
|----------|----------------------------------|---------------------------------|--------|
| stringArray | 字符串数组，若输入为 `null` 或 `undefined`，将返回空数组 | `T[] | null | undefined`      | 无     |
| key      | 要设置的属性名，默认为 'key'    | `string`                        | `'key'`|
| excludeNil| 是否排除 null 和 undefined，默认为 false | `boolean`                       | `false`|

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Array<{ [K in typeof key]: T }>` | 返回对象数组，每个对象包含指定的属性，对应数组中的字符串 |

#### <divider-desc /> {#desc-arrayToObject}

- 将字符串数组转换为对象数组，支持可选地排除 null 的项
</div>

### toMappedArray

将对象数组映射为指定格式

<div class="buzzts-border">

#### <divider-base /> {#base-toMappedArray}

<toMappedArray />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/toMappedArray.vue

</details>

#### <divider-param /> {#param-toMappedArray}

| 参数属性     | 说明                          | 类型                                                          | 默认值          |
|--------------|-------------------------------|---------------------------------------------------------------|------------------|
| items        | 输入的对象数组                | `Array<{ [key: string]: any }>` | `null` 或 `undefined` |
| options      | 选项对象                      | `{ inKeyField?: string; inValueField?: string; outKeyField?: string; outValueField?: string; includeKey?: boolean; includeValue?: boolean; }` | {}               |
| options.inKeyField | 输入的 key 字段名         | `string`                                                        | `key`            |
| options.inValueField | 输入的 value 字段名     | `string`                                                        | `value`          |
| options.outKeyField | 输出的 key 字段名       | `string`                                                        | `key`            |
| options.outValueField | 输出的 value 字段名   | `string`                                                        | `value`          |
| options.includeKey | 是否输出 key             | `boolean`                                                       | `true`             |
| options.includeValue | 是否输出 value         | `boolean`                                                       | `true`            |
| options.excludeNil| 是否排除 `null` 和 `undefined`，默认为 `false` | `boolean`                       | `false` |

| 返回值                   | 说明                                   |
|------------------------|----------------------------------------|
| `Array<{ [outKeyField]: string; label?: string; [outValueField]?: string }>` | 返回映射后的数组 |

#### <divider-desc /> {#desc-toMappedArray}

- 将输入的对象数组转换为指定格式的数组。
- 如果输入为 `null` 或 `undefined`，返回一个空数组。
- 通过可选的 `options` 对象，用户可以自定义输入和输出字段名，以及是否包含 key 和 value 字段。

</div>

### findValueByKey

根据键和值查找对象的对应值

<div class="buzzts-border">

#### <divider-base /> {#base-findValueByKey}

<findValueByKey />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/findValueByKey.vue

</details>

#### <divider-param /> {#param-findValueByKey}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| items    | 输入的对象数组 | `Array<{ [key: string]: any }>` | `null` |
| key      | 要查找的键 | string | 无     |
| value    | 要查找的值 | any   | 无     |
| returnKey| 要返回的特定键 | string | undefined |

| 返回值   | 说明                   |
|----------|------------------------|
| `any | null` | 返回匹配的值或 `null` |

#### <divider-desc /> {#desc-findValueByKey}

- 根据指定的键和值在输入的对象数组中查找匹配的值。
- 如果输入为 `null` 或未找到匹配项，返回 `null`。
- 如果提供了 `returnKey`，则返回匹配对象中指定键的值；否则返回整个匹配对象。

</div>

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

### getBetween

通用区间遍历函数，支持数字、日期、字符等多种类型

<div class="buzzts-border">

#### <divider-base /> {#base-getBetween}

<getBetween />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/getBetween.vue

</details>

#### <divider-param /> {#param-getBetween}

| 参数属性 | 说明                         | 类型                                  | 默认值 |
|----------|------------------------------|-------------------------------------|--------|
| start    | 起点                         | T                                   | 无     |
| end      | 终点                         | T                                   | 无     |
| options  | 递增规则和比较规则           | `{ step?: number; compare?: (current: T, end: T) => boolean; next: (current: T, step: number) => T; }` | 无     |

| 返回值   | 说明                           |
|----------|--------------------------------|
| `T[] \| null` | 包含起止的所有值数组，输入无效返回 null |

#### <divider-desc /> {#desc-getBetween}

- 支持数字、日期、字符等区间遍历
- 通过自定义比较和递增函数灵活控制遍历规则

</div>

### mergeObject

深拷贝合并对象，优先使用 source 中的值覆盖 defaults

<div class="buzzts-border">

#### <divider-base /> {#base-mergeObject}

<mergeObject />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/mergeObject.vue

</details>

#### <divider-param /> {#param-mergeObject}

| 参数属性 | 说明           | 类型    | 默认值 |
|----------|----------------|---------|--------|
| source   | 外部的参数对象 | object? | 无     |
| defaults | 默认参数对象   | object? | 无     |

| 返回值 | 说明         |
|--------|--------------|
| object | 合并后的新对象 |

#### <divider-desc /> {#desc-mergeObject}

- 深拷贝合并对象，递归合并普通对象
- 跳过 null 值，防止原型污染

</div>

### deepClone

深度复制对象，支持循环引用、日期、正则、原型链和属性描述符

<div class="buzzts-border">

#### <divider-base /> {#base-deepClone}

<deepClone />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/deepClone.vue

</details>

#### <divider-param /> {#param-deepClone}

| 参数属性 | 说明                      | 类型                  | 默认值      |
|----------|---------------------------|-----------------------|-------------|
| obj      | 将要复制的对象            | T                     | 无          |
| hash     | 用于处理循环引用的哈希表  | `WeakMap<any, any>?`  | 新建 WeakMap |

| 返回值 | 说明         |
|--------|--------------|
| T      | 复制后的对象 |

#### <divider-desc /> {#desc-deepClone}

- 支持各种复杂类型的深度复制
- 处理循环引用，保证复制安全

</div>

### upperMoney

现金额转大写

<div class="buzzts-border">

#### <divider-base /> {#base-upperMoney}

<upperMoney />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/upperMoney.vue

</details>

#### <divider-param /> {#param-upperMoney}

| 参数属性 | 说明 | 类型   | 默认值 |
|----------|------|--------|--------|
| n        | 数字 | number | 无     |

| 返回值 | 说明     |
|--------|----------|
| string | 转换后的大写金额字符串 |

#### <divider-desc /> {#desc-upperMoney}

- 支持正负数和小数
- 处理零和整的特殊情况

</div>

### intToLowerChinese

数字转中文(小写)

<div class="buzzts-border">

#### <divider-base /> {#base-intToLowerChinese}

<intToLowerChinese />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/intToLowerChinese.vue

</details>

#### <divider-param /> {#param-intToLowerChinese}

| 参数属性 | 说明             | 类型               | 默认值 |
|----------|------------------|--------------------|--------|
| value    | 非负整数数字或字符串 | `string \| number` | 无     |

| 返回值 | 说明         |
|--------|--------------|
| string | 转换后的中文字符串 |

#### <divider-desc /> {#desc-intToLowerChinese}

- 支持大数字转换
- 输入必须为非负整数字符串或数字，非法输入抛错

</div>

### sumAverage

计算数组平均值

<div class="buzzts-border">

#### <divider-base /> {#base-sumAverage}

<sumAverage />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/sumAverage.vue

</details>

#### <divider-param /> {#param-sumAverage}

| 参数属性  | 说明     | 类型       | 默认值 |
|-----------|----------|------------|--------|
| numberArr | 数字数组 | `number[]` | 无     |

| 返回值 | 说明   |
|--------|--------|
| number | 数组平均值 |

#### <divider-desc /> {#desc-sumAverage}

- 计算数组所有元素的平均值
- 输入数组为空时需处理

</div>

### getDistance

计算两坐标点之间的距离

<div class="buzzts-border">

#### <divider-base /> {#base-getDistance}

<getDistance />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/getDistance.vue

</details>

#### <divider-param /> {#param-getDistance}

| 参数属性 | 说明       | 类型       | 默认值 |
|----------|------------|------------|--------|
| point1   | 第一个点坐标 | `{x:number,y:number}` | 无     |
| point2   | 第二个点坐标 | `{x:number,y:number}` | 无     |

| 返回值 | 说明   |
|--------|--------|
| number | 两点距离 |

#### <divider-desc /> {#desc-getDistance}

- 使用欧几里得距离公式计算二维空间两点距离

</div>

### chunkArray

将数组分成指定数量的块（尽量平均分配）

<div class="buzzts-border">

#### <divider-base /> {#base-chunkArray}

<chunkArray />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/chunkArray.vue

</details>

#### <divider-param /> {#param-chunkArray}

| 参数属性   | 说明                     | 类型     | 默认值 |
|------------|--------------------------|----------|--------|
| data       | 要分块的数组             | `T[]`    | 无     |
| chunkCount | 分块数量，正整数且不超过数组长度 | `number` | 无     |

| 返回值     | 说明                   |
|------------|------------------------|
| `T[][]`    | 分块后的二维数组       |

#### <divider-desc /> {#desc-chunkArray}

- 将数组分成指定数量的块，尽量平均分配元素
- 如果分块数大于数组长度，每个元素单独成块
- 参数校验失败时会抛错

</div>

### getPercentage

计算百分比

<div class="buzzts-border">

#### <divider-base /> {#base-getPercentage}

<getPercentage />

<details>
<summary>查看代码</summary>

<<< @/utils/mathx/getPercentage.vue

</details>

#### <divider-param /> {#param-getPercentage}

| 参数属性     | 说明             | 类型     | 默认值 |
|--------------|------------------|----------|--------|
| part         | 当前值           | `number` | 无     |
| total        | 总值             | `number` | 无     |
| decimalPlaces | 保留小数位数，默认2位 | `number` | `2`    |

| 返回值       | 说明                   |
|--------------|------------------------|
| `string`     | 百分比字符串，如 "50.00%" |

#### <divider-desc /> {#desc-getPercentage}

- 计算百分比，返回格式化字符串，默认保留两位小数
- 总值为0时返回0%
- 参数非数字时抛异常

</div>
