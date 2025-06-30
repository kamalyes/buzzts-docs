<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(15)

import typeasy from "./typeasy.vue"
import typeasyIs from "./typeasyIs.vue"
import typeasyIsPrimitive from "./typeasyIsPrimitive.vue"
import isUndefined from "./isUndefined.vue"
import isNull from "./isNull.vue"
import isNil from "./isNil.vue"
import isBoolean from "./isBoolean.vue"
import isString from "./isString.vue"
import isEmpty from "./isEmpty.vue"
import isFunction from "./isFunction.vue"
import isArray from "./isArray.vue"
import isObject from "./isObject.vue"
import isSymbol from "./isSymbol.vue"
import isBigInt from "./isBigInt.vue"
import getTypeOf from "./getTypeOf.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
类型校验工具集
:::

### isUndefined

判断是否为 undefined

<div class="buzzts-border">

#### <divider-base /> {#base-isUndefined}

<isUndefined />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isUndefined.vue

</details>

#### <divider-param /> {#param-isUndefined}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为 undefined |

#### <divider-desc /> {#desc-isUndefined}

- 判断传入值是否严格等于 `undefined`

</div>

### isNull

判断是否为 null

<div class="buzzts-border">

#### <divider-base /> {#base-isNull}

<isNull />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isNull.vue

</details>

#### <divider-param /> {#param-isNull}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明        |
|----------|-------------|
| boolean  | 是否为 null |

#### <divider-desc /> {#desc-isNull}

- 判断传入值是否严格等于 `null`

</div>

### isNil

判断是否为 null 或 undefined

<div class="buzzts-border">

#### <divider-base /> {#base-isNil}

<isNil />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isNil.vue

</details>

#### <divider-param /> {#param-isNil}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明                |
|----------|---------------------|
| boolean  | 是否为 null 或 undefined |

#### <divider-desc /> {#desc-isNil}

- 判断传入值是否为 `null` 或 `undefined`

</div>

### isBoolean

判断是否为布尔值

<div class="buzzts-border">

#### <divider-base /> {#base-isBoolean}

<isBoolean />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isBoolean.vue

</details>

#### <divider-param /> {#param-isBoolean}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为布尔值    |

#### <divider-desc /> {#desc-isBoolean}

- 判断传入值类型是否为布尔值

</div>


### isString

判断是否为字符串

<div class="buzzts-border">

#### <divider-base /> {#base-isString}

<isString />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isString.vue

</details>

#### <divider-param /> {#param-isString}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为字符串    |

#### <divider-desc /> {#desc-isString}

- 判断传入值类型是否为字符串

</div>

### isEmpty

判断是否为空值（null、undefined、空字符串、空数组、空对象）

<div class="buzzts-border">

#### <divider-base /> {#base-isEmpty}

<isEmpty />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isEmpty.vue

</details>

#### <divider-param /> {#param-isEmpty}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为空值      |

#### <divider-desc /> {#desc-isEmpty}

- 判断传入值是否为 null、undefined、空字符串（含空白）、空数组或空对象（非内置对象）

</div>

### isFunction

判断是否为函数

<div class="buzzts-border">

#### <divider-base /> {#base-isFunction}

<isFunction />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isFunction.vue

</details>

#### <divider-param /> {#param-isFunction}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为函数      |

#### <divider-desc /> {#desc-isFunction}

- 判断传入值类型是否为函数

</div>

### isArray

判断是否为数组

<div class="buzzts-border">

#### <divider-base /> {#base-isArray}

<isArray />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isArray.vue

</details>

#### <divider-param /> {#param-isArray}

| 参数属性 | 说明   | 类型 | 默认值 |
|----------|--------|------|--------|
| val      | 任意值 | any  | 无     |

| 返回值   | 说明     |
|----------|----------|
| boolean  | 是否数组 |

#### <divider-desc /> {#desc-isArray}

- 判断传入的值是否为数组
</div>

### isObject

判断是否为普通对象（非 null，非数组）

<div class="buzzts-border">

#### <divider-base /> {#base-isObject}

<isObject />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isObject.vue

</details>

#### <divider-param /> {#param-isObject}

| 参数属性 | 说明   | 类型 | 默认值 |
|----------|--------|------|--------|
| val      | 任意值 | any  | 无     |

| 返回值   | 说明       |
|----------|------------|
| boolean  | 是否普通对象 |

#### <divider-desc /> {#desc-isObject}

- 判断传入的值是否为普通对象（非 null，非数组）
</div>


### isSymbol

判断是否为 Symbol 类型

<div class="buzzts-border">

#### <divider-base /> {#base-isSymbol}

<isSymbol />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isSymbol.vue

</details>

#### <divider-param /> {#param-isSymbol}

| 参数属性 | 说明       | 类型 | 默认值 |
|----------|------------|------|--------|
| val      | 任意值     | any  | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否 Symbol 类型 |

#### <divider-desc /> {#desc-isSymbol}

- 判断传入值是否为 Symbol 类型
- 示例：
  - `isSymbol(Symbol()) // true`
  - `isSymbol('abc') // false`

</div>

### isBigInt

判断是否为 BigInt 类型

<div class="buzzts-border">

#### <divider-base /> {#base-isBigInt}

<isBigInt />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/isBigInt.vue

</details>

#### <divider-param /> {#param-isBigInt}

| 参数属性 | 说明   | 类型   | 默认值    |
|----------|--------|--------|-----------|
| val      | 任意值 | any    | 无        |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否 BigInt 类型|

#### <divider-desc /> {#desc-isBigInt}

- 判断输入值是否为 BigInt 类型
- 示例：
  - `isBigInt(BigInt(123)) // true`
  - `isBigInt(123) // false`

</div>

### getTypeOf

获取参数类型，支持基本类型和常见内置对象类型

<div class="buzzts-border">

#### <divider-base /> {#base-getTypeOf}

<getTypeOf />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/getTypeOf.vue

</details>

#### <divider-param /> {#param-getTypeOf}

| 参数属性 | 说明           | 类型    | 默认值 |
|----------|----------------|---------|--------|
| param    | 需要判断类型的参数 | unknown | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `string` | 返回参数的具体类型名称（首字母大写）|

#### <divider-desc /> {#desc-getTypeOf}

- 利用 `Object.prototype.toString` 获取类型标签
- 返回首字母大写的类型名称，如 `"String"`, `"Array"`, `"AsyncFunction"` 等
- 示例：
  - `getTypeOf('abc') // "String"`
  - `getTypeOf([]) // "Array"`

</div>

### typeasy

基础数据类型检测工具（支持 15+ 常见类型识别）

<div class="buzzts-border">

#### <divider-base /> {#base-typeasy}

<typeasy />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/typeasy.vue

</details>

#### <divider-param /> {#param-typeasy}

| 参数属性 | 说明         | 类型    | 默认值 |
|----------|--------------|---------|--------|
| data     | 需要检测类型的值 | any     | 无     |

| 返回值   | 说明                     |
|----------|--------------------------|
| `string` | 返回全小写的类型字符串       |

#### <divider-desc /> {#desc-typeasy}

- 支持 null、undefined、NaN、Infinity、-0、数组、对象、正则、日期、函数、类、Map、Set、Symbol、BigInt 等多种类型的检测。

</div>

### typeasy.is

精确类型验证工具

<div class="buzzts-border">

#### <divider-base /> {#base-typeasy-is}

<typeasy-is />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/typeasyIs.vue

</details>

#### <divider-param /> {#param-typeasy-is}

| 参数属性 | 说明         | 类型    | 默认值 |
|----------|--------------|---------|--------|
| data     | 要检测的值     | any     | 无     |
| type     | 预期的类型字符串 | string  | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 类型是否匹配     |

#### <divider-desc /> {#desc-typeasy-is}

- 判断给定数据是否严格匹配预期类型字符串。

</div>

### typeasy.isPrimitive

检测是否为原始类型（非引用类型）

<div class="buzzts-border">

#### <divider-base /> {#base-typeasy-isPrimitive}

<typeasy-isPrimitive />

<details>
<summary>查看代码</summary>

<<< @/utils/typed/typeasyIsPrimitive.vue

</details>

#### <divider-param /> {#param-typeasy-isPrimitive}

| 参数属性 | 说明         | 类型    | 默认值 |
|----------|--------------|---------|--------|
| data     | 要检测的值     | any     | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否为原始类型   |

#### <divider-desc /> {#desc-typeasy-isPrimitive}

- 判断数据是否为 JavaScript 原始类型（包括 null、undefined、number、string、boolean、symbol、bigint 等）。

</div>
