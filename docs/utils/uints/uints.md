<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(6)

import upperMoney from "./upperMoney.vue";
import rmbFormatter from "./rmbFormatter.vue";
import intToLowerChinese from "./intToLowerChinese.vue"
import sumAverage from "./sumAverage.vue"
import getDistance from "./getDistance.vue"
import getPercentage from "./getPercentage.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理数据工具集
:::

### upperMoney

现金额转大写

<div class="buzzts-border">

#### <divider-base /> {#base-upperMoney}

<upperMoney />

<details>
<summary>查看代码</summary>

<<< @/utils/uints/upperMoney.vue

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


### RmbFormatter

RmbFormatter 组件用于处理人民币金额单位之间的转换，包括元、角、分和厘。

<div class="buzzts-border">

#### <divider-base /> {#base-rmbFormatter}

<rmbFormatter />

<details>
<summary>查看代码</summary>

<<< @/utils/uints/rmbFormatter.vue

</details>

#### <divider-param /> {#param-rmbFormatter}

| 参数属性 | 说明                               | 类型                       | 默认值 |
|----------|------------------------------------|----------------------------|--------|
| amount   | 需要设置的金额                     | `number \| string`           | 无     |
| from     | 当前金额的单位                     | `'yuan' \| 'jiao' \| 'cents' \| 'li'` | 无     |
| precision| 用户自定义的精度                   | `number`                     | 2      |

| 返回值 | 说明                   |
|--------|------------------------|
| void   | 设置金额和单位后无返回值 |

#### <divider-desc /> {#desc-rmbFormatter}

- rmbFormatter 组件支持人民币金额的单位转换。
- 支持的单位包括元（yuan）、角（jiao）、分（cents）和厘（li）。
- 用户可以设置自定义精度，默认精度为两位小数, 需注意在不同的转换情况下精度会直接影响结果。
- 提供金额的解析和转换功能，确保金额以分为单位进行存储和计算。
</div>

### intToLowerChinese

数字转中文(小写)

<div class="buzzts-border">

#### <divider-base /> {#base-intToLowerChinese}

<intToLowerChinese />

<details>
<summary>查看代码</summary>

<<< @/utils/uints/intToLowerChinese.vue

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

<<< @/utils/uints/sumAverage.vue

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

<<< @/utils/uints/getDistance.vue

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

### getPercentage

计算百分比

<div class="buzzts-border">

#### <divider-base /> {#base-getPercentage}

<getPercentage />

<details>
<summary>查看代码</summary>

<<< @/utils/uints/getPercentage.vue

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
