<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(17)

import isValidDate from "./isValidDate.vue"
import toDate from "./toDate.vue"
import addTime from "./addTime.vue"
import getDayOfWeek from "./getDayOfWeek.vue"
import diffDaysWithDecimal from "./diffDaysWithDecimal.vue"
import getDateInfo from "./getDateInfo.vue"
import getWeekdayCountInMonth from "./getWeekdayCountInMonth.vue"
import getUnixTimestamp from "./getUnixTimestamp.vue"
import timestampToDate from "./timestampToDate.vue"
import formatDate from "./formatDate.vue"
import formatDuration from "./formatDuration.vue"
import compareTwoDates from "./compareTwoDates.vue"
import isBetween from "./isBetween.vue"
import isLeapYear from "./isLeapYear.vue"
import isSameDay from "./isSameDay.vue"
import isWeekend from "./isWeekend.vue"
import getBoundaryOfDay from "./getBoundaryOfDay.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理时间工具集
:::

### toDate

将多种类型的日期输入统一转换为 Date 对象，方便内部函数调用

<div class="buzzts-border">

#### <divider-base /> {#base-toDate}

<toDate />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/toDate.vue

</details>

#### <divider-param /> {#param-toDate}

| 参数属性 | 说明         | 类型          | 默认值 |
|----------|--------------|---------------|--------|
| d        | 任意支持的日期输入 | `DateInput`   | 无     |

| 返回值   | 说明                       |
|----------|----------------------------|
| `Date \| null` | 有效的 Date 对象，解析失败返回 null |

#### <divider-desc /> {#desc-toDate}

- 支持 `Date` 对象、时间戳（秒或毫秒）、日期字符串等多种输入

- 纯日期格式（YYYY-MM-DD）强制加上 UTC 时区标识，避免时区偏差

- 解析失败返回 `null`

- 方便内部统一处理日期输入

</div>

### addTime

统一处理日期加时间的函数，支持增加天、小时、分钟、秒等多种时间单位

<div class="buzzts-border">

#### <divider-base /> {#base-addTime}

<addTime />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/addTime.vue

</details>

#### <divider-param /> {#param-addTime}

| 参数属性 | 说明                     | 类型                                       | 默认值 |
|----------|--------------------------|--------------------------------------------|--------|
| date     | 基准日期                 | `DateInput`（支持 Date、时间戳、字符串） | 无     |
| amount   | 增加的时间数量，可为负数 | `number`                                   | 无     |
| unit     | 时间单位                 | `'Date' \| 'Hours' \| 'Minutes' \| 'Seconds'` | 无     |

| 返回值   | 说明                       |
|----------|----------------------------|
| `Date \| null` | 返回新的日期对象，输入无效返回 `null` |

#### <divider-desc /> {#desc-addTime}

- 通过统一入口函数 `addTime` 实现日期加时间功能
- 支持多种时间单位，方便灵活调用
- 输入支持多种日期格式，内部统一处理解析
- 便捷函数 `addDays`、`addHours`、`addMinutes`、`addSeconds` 简化调用

</div>

### getDayOfWeek

获取日期对应的星期（0-周日，6-周六）

<div class="buzzts-border">

#### <divider-base /> {#base-getDayOfWeek}

<getDayOfWeek />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/getDayOfWeek.vue

</details>

#### <divider-param /> {#param-getDayOfWeek}

| 参数属性 | 说明     | 类型       | 默认值 |
|----------|----------|------------|--------|
| date     | 指定日期 | DateInput  | 无     |

| 返回值       | 说明                                 |
|--------------|------------------------------------|
| `number \| null` | 日期对应的星期（0-周日，6-周六），输入无效返回 null |

#### <divider-desc /> {#desc-getDayOfWeek}

- 获取日期对应的星期（0-周日，6-周六），输入无效返回 null

</div>


### getBoundaryOfDay

获取指定日期当天的开始时间（00:00:00）

<div class="buzzts-border">

#### <divider-base /> {#base-getBoundaryOfDay}

<getBoundaryOfDay />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/getBoundaryOfDay.vue

</details>

#### <divider-param /> {#param-getBoundaryOfDay}

| 参数属性 | 说明             | 类型               | 默认值 |
|----------|------------------|--------------------|--------|
| date     | 指定日期         | `DateInput`        | 无     |

| 返回值   | 说明                               |
|----------|----------------------------------|
| `Date \| null` | 返回当天开始时间，输入无效返回 `null` |

#### <divider-desc /> {#desc-getBoundaryOfDay}

- 通过调用 `getBoundaryOfDay` 获取当天开始时间
- 支持多种日期格式输入，内部统一解析
- 返回的`start`时间为当天 00:00:00
- 返回的`end`时间为当天 23:59:59.999
- 便捷函数 `startOfDay`、`endOfDay` 简化调用

</div>

### diffDaysWithDecimal

计算两个日期之间相差的完整天数（绝对值）

<div class="buzzts-border">

#### <divider-base /> {#base-diffDaysWithDecimal}

<diffDaysWithDecimal />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/diffDaysWithDecimal.vue

</details>

#### <divider-param /> {#param-diffDaysWithDecimal}

| 参数属性 | 说明     | 类型       | 默认值 |
|----------|----------|------------|--------|
| dateA    | 日期A    | DateInput  | 无     |
| dateB    | 日期B    | DateInput  | 无     |

| 返回值       | 说明                                 |
|--------------|------------------------------------|
| `number \| null` | 两日期之间相差的完整天数，输入无效返回 null |

#### <divider-desc /> {#desc-diffDaysWithDecimal}

- 计算两个日期之间相差的天数，结果为绝对值，输入无效时返回 null。

</div>

### getDateInfo

获取日期的详细信息，包括年份、月份、日、小时、分钟、秒和毫秒

<div class="buzzts-border">

#### <divider-base /> {#base-getDateInfo}

<getDateInfo />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/getDateInfo.vue

</details>

#### <divider-param /> {#param-getDateInfo}

| 参数属性 | 说明     | 类型      | 默认值 |
|----------|----------|-----------|--------|
| date     | 指定日期 | DateInput | 无     |

| 返回值       | 说明                                 |
|--------------|------------------------------------|
| `DateInfo \| null` | 包含年、月、日、时、分、秒、毫秒的对象，输入无效返回 null |

#### <divider-desc /> {#desc-getDateInfo}

- 获取传入日期的各项详细信息：
- 年份（`year`），对应 `getYear()`，输入无效时返回 null
- 月份（`month`），对应 `getMonth()`，范围1-12，输入无效时返回 null
- 日（`day`），对应 `getDay()`，范围1-31，输入无效时返回 null
- 小时（`hours`），对应 `getHours()`，范围0-23，输入无效时返回 null
- 分钟（`minutes`），对应 `getMinutes()`，范围0-59，输入无效时返回 null
- 秒（`seconds`），对应 `getSeconds()`，范围0-59，输入无效时返回 null
- 毫秒（`milliseconds`），对应 `getMilliseconds()`，范围0-999，输入无效时返回 null

</div>

### getWeekdayCountInMonth

计算指定日期所在月份中，每个星期几出现的次数

<div class="buzzts-border">

#### <divider-base /> {#base-getWeekdayCountInMonth}

<getWeekdayCountInMonth />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/getWeekdayCountInMonth.vue

</details>

#### <divider-param /> {#param-getWeekdayCountInMonth}

| 参数属性       | 说明               | 类型       | 默认值               |
|----------------|--------------------|------------|----------------------|
| date           | 指定日期           | Date       | 当前日期 new Date()  |

| 返回值   | 说明                           |
|----------|--------------------------------|
| `WeekdayCount \|null` | 该月中每个星期几出现的次数对象，输入无效返回 null |

#### <divider-desc /> {#desc-getWeekdayCountInMonth}

- 计算指定日期所在月份中，每个星期几出现的次数，返回包含 sunday 到 saturday 的计数对象。

</div>

### getUnixTimestamp

获取指定日期的 Unix 时间戳（秒）

<div class="buzzts-border">

#### <divider-base /> {#base-getUnixTimestamp}

<getUnixTimestamp />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/getUnixTimestamp.vue

</details>

#### <divider-param /> {#param-getUnixTimestamp}

| 参数属性      | 说明               | 类型       | 默认值            |
|---------------|--------------------|------------|-------------------|
| date          | 需要转换的日期     | DateInput  | 当前日期          |

| 返回值       | 说明                       |
|--------------|----------------------------|
| `number | null` | Unix 时间戳（秒），输入无效返回 null |

#### <divider-desc /> {#desc-getUnixTimestamp}

- 获取指定日期的 Unix 时间戳（秒）。

</div>

### timestampToDate

将秒或毫秒时间戳转换为 Date 对象

<div class="buzzts-border">

#### <divider-base /> {#base-timestampToDate}

<timestampToDate />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/timestampToDate.vue

</details>

#### <divider-param /> {#param-timestampToDate}

| 参数属性      | 说明               | 类型               |
|---------------|--------------------|--------------------|
| timestamp     | 时间戳（秒或毫秒） | number | string |

| 返回值       | 说明                       |
|--------------|----------------------------|
| `Date | null` | 转换后的 Date 对象，失败返回 null |

#### <divider-desc /> {#desc-timestampToDate}

- 将秒或毫秒时间戳转换为 Date 对象。

</div>

### formatDate

根据格式字符串格式化日期，支持常用占位符

<div class="buzzts-border">

#### <divider-base /> {#base-formatDate}

<formatDate />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/formatDate.vue

</details>

#### <divider-param /> {#param-formatDate}

| 参数属性 | 说明               | 类型      | 默认值       |
|----------|--------------------|-----------|--------------|
| format   | 格式字符串，如 'YYYY-MM-DD HH:mm:ss' | string | 无           |
| date     | 需要格式化的日期   | DateInput | new Date()   |

| 返回值   | 说明                     |
|----------|--------------------------|
| `string | null` | 格式化后的字符串，输入无效返回 null |

#### <divider-desc /> {#desc-formatDate}

- 根据格式字符串格式化日期，支持常用占位符。

</div>

### formatDuration

将秒数格式化为 HH:mm:ss 格式字符串

<div class="buzzts-border">

#### <divider-base /> {#base-formatDuration}

<formatDuration />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/formatDuration.vue

</details>

#### <divider-param /> {#param-formatDuration}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| seconds  | 持续时间，单位秒 | number | 无     |

| 返回值   | 说明                     |
|----------|--------------------------|
| `string` | 格式化的持续时间，如 '01:23:36' |

#### <divider-desc /> {#desc-formatDuration}

- 将秒数格式化为 HH:mm:ss 格式字符串。

</div>

### compareTwoDates

比较两个日期，判断第一个日期是否在第二个日期之前或之后

<div class="buzzts-border">

#### <divider-base /> {#base-compareTwoDates}

<compareTwoDates />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/compareTwoDates.vue

</details>

#### <divider-param /> {#param-compareTwoDates}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| dateA    | 第一个日期 | DateInput | 无     |
| dateB    | 第二个日期 | DateInput | 无     |
| type     | 比较类型   | `before`,`after` | `before` | 

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean|null`| 返回比较结果，true 或 false；如果任一日期无效，则返回 null |

#### <divider-desc /> {#desc-compareTwoDates}

- 比较两个日期，判断第一个日期是否在第二个日期之前或之后

</div>

### isBetween

判断目标日期是否位于起始日期和结束日期之间（包含边界）

<div class="buzzts-border">

#### <divider-base /> {#base-isBetween}

<isBetween />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/isBetween.vue

</details>

#### <divider-param /> {#param-isBetween}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| target   | 目标日期   | DateInput | 无     |
| start    | 起始日期   | DateInput | 无     |
| end      | 结束日期   | DateInput | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean|null` | 返回目标日期是否在区间内，true 或 false；如果任一日期无效，则返回 null |

#### <divider-desc /> {#desc-isBetween}

- 判断目标日期是否位于起始日期和结束日期之间（包含边界）

</div>

### isLeapYear

判断指定年份是否为闰年

<div class="buzzts-border">

#### <divider-base /> {#base-isLeapYear}

<isLeapYear />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/isLeapYear.vue

</details>

#### <divider-param /> {#param-isLeapYear}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| year     | 年份       | number | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean` | 是否为闰年 |

#### <divider-desc /> {#desc-isLeapYear}

- 判断指定年份是否为闰年

</div>

### isSameDay

判断两个日期是否是同一天，输入无效返回 null

<div class="buzzts-border">

#### <divider-base /> {#base-isSameDay}

<isSameDay />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/isSameDay.vue

</details>

#### <divider-param /> {#param-isSameDay}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| dateA    | 第一个日期 | DateInput | 无     |
| dateB    | 第二个日期 | DateInput | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean|null` | 是否为同一天，输入无效返回 null |

#### <divider-desc /> {#desc-isSameDay}

- 判断两个日期是否是同一天

</div>


### isWeekend

判断日期是否为周末（周六或周日），输入无效返回 null

<div class="buzzts-border">

#### <divider-base /> {#base-isWeekend}

<isWeekend />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/isWeekend.vue

</details>

#### <divider-param /> {#param-isWeekend}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| date     | 日期       | DateInput | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean|null` | 是否为周末，输入无效返回 null |

#### <divider-desc /> {#desc-isWeekend}

- 判断日期是否为周末（周六或周日），输入无效返回 null

</div>


### isValidDate

判断一个对象是否为有效的日期对象

<div class="buzzts-border">

#### <divider-base /> {#base-isValidDate}

<isValidDate />

<details>
<summary>查看代码</summary>

<<< @/utils/datetime/isValidDate.vue

</details>

#### <divider-param /> {#param-isValidDate}

| 参数属性 | 说明       | 类型 | 默认值 |
|----------|------------|------|--------|
| date     | 需要判断的对象 | any  | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否为有效的 Date 对象 |

#### <divider-desc /> {#desc-isValidDate}

- 判断一个对象是否为有效的日期对象

- 例如 `new Date()` 返回 `true`，`new Date('invalid')` 返回 `false`

</div>