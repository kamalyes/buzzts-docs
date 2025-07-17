<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(1)

import loggerx from "./loggerx.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
日志处理
:::

### Logger

表示一个日志记录器，提供多种日志记录功能，包括不同的日志等级、颜色输出、时间戳、持久化存储等。

<div class="buzzts-border">

#### <divider-base /> {#base-logger}

<loggerx />

<details>
<summary>查看代码</summary>

<<< @/utils/logger/loggerx.vue

</details>

#### <divider-param /> {#param-logger}

| 参数属性               | 说明                                                         | 类型                       | 默认值                     |
|------------------------|--------------------------------------------------------------|----------------------------|----------------------------|
| `logLevel`             | 当前的日志等级，用于控制哪些日志消息会被记录               | `LogLevel`                 | -                          |
| `ignore`               | 可选的回调函数，用于决定是否忽略某条日志                   | `(log: string \| Error \| LogEntry, logLevel: LogLevel, persistent?: boolean) => boolean` | -                          |
| `colors`               | 是否启用颜色输出，默认为 `true` 当 stdout 是 TTY 且未禁用颜色 | `boolean`                  | `true`                     |
| `emoji`                | 是否启用 Emoji，默认为根据操作系统决定                     | `boolean`                  | 根据操作系统决定           |
| `maxLogs`              | 最大日志数量，超过此数量的日志将被删除                     | `number`                   | `100`                      |
| `timestamp`            | 是否在日志消息中包含时间戳，默认为 `true`                    | `boolean`                  | `true`                     |
| `persistent`           | 是否持久化日志，持久化日志意味着日志不会被清除             | `boolean`                  | `false`                    |
| `successIcon`          | 自定义成功图标，默认为根据是否启用 Emoji 决定              | `string`                   | 根据是否启用 Emoji 决定    |
| `warningIcon`          | 自定义警告图标，默认为根据是否启用 Emoji 决定              | `string`                   | 根据是否启用 Emoji 决定    |
| `errorIcon`            | 自定义错误图标，默认为根据是否启用 Emoji 决定              | `string`                   | 根据是否启用 Emoji 决定    |
| `fatalIcon`            | 自定义致命错误图标，默认为错误图标                         | `string`                   | 错误图标                   |

| 返回值   | 说明                               |
|----------|------------------------------------|
| `Logger` | 实例化的日志记录器对象             |

#### <divider-desc /> {#desc-logger}

- 提供多种日志记录功能，包括信息、警告、错误、成功和调试日志。
- 自动处理日志等级，确保只记录指定等级及以上的日志。
- 支持持久化存储日志到 `localStorage`，以便后续查看, `maxLogs` 属性用于限制存储的最大日志数量，超过该数量的日志将被删除，以避免存储过满的问题。
- 支持进度指示器，能够启动、更新和停止进度显示。
- 支持分组日志输出，便于组织和查看相关日志。
- 提供清除日志的功能，能够清空控制台输出。
- 支持边界值安全，确保在特定情况下（如相同的最小值和最大值）不会抛出错误。

</div>