---
description: provider 通过 prefix cache 缓存的 input token，来自先前请求，按远低费率计费。
---

[Input tokens](./Input%20tokens.md)（输入 token）中，[provider](./Model%20provider.md)（提供商）已从此前一次 [model provider request](./Model%20provider%20request.md)（模型提供商请求）缓存下来的部分，因此不必重新处理。连续请求共享前缀时，provider 通过 [prefix cache](./Prefix%20cache.md)（前缀缓存）复用先前做过的处理，缓存部分按低得多的费率计费。让长 [sessions](./Session.md)（会话）负担得起的正是这一机制：没有它，每个 [turn](./Turn.md)（轮次）都要为整段历史重新付全款。

这件事重要，是因为 session 按这种方式计费。[model](./Model.md)（模型）是 [stateless](./Stateless.md)（无状态）的，所以每个请求都要把整段对话重发一遍——[system prompt](./System%20prompt.md)（系统提示词）、每条消息、每个 [tool result](./Tool%20result.md)（工具结果）——全部作为 input token。到第五十个 turn，每个请求都背着五十轮历史，每次都要按全价为整段历史付费。缓存改变了这笔账：provider 在相同前缀里已经处理过的 token（词元），按 cache token（缓存 token）计费，常常只有输入费率的十分之一或更低。在长 session 里，你发送的大部分内容都是 cache token，账单因此保持在合理范围。

一个例子说明哪些 token 会被缓存、哪些不会。每个字母代表一块对话内容；每个请求都发送到目前为止的对话：

| 请求发送 | 已缓存 | 按全价计费 | 原因 |
| ------------- | ------- | ------------------- | ------------------------------------------------- |
| `AB`          | 无      | `AB`                | 首次请求——没有可匹配的前缀 |
| `ABC`         | `AB`    | `C`                 | `AB` 是上一请求的精确前缀 |
| `ABCD`        | `ABC`   | `D`                 | 前缀仍完整 |
| `AXCD`        | `A`     | `XCD`               | 一次编辑把 `B` 改成了 `X`；匹配在那里失败 |

缓存有一个特定的脆弱点：它匹配的是精确前缀。对话中靠前的地方一变——[harness](./Harness.md)（运行框架）重排了内容、时间戳更新了、某个文件的表示变了——缓存从那一点起全部未命中，其后的一切按输入全价计费。缓存在闲置几分钟后也会过期，所以长时间暂停后恢复的 session 会把历史重付一次。当 session 的费用在没有明显原因的情况下跳涨，先在用量报告里对比 cache token 和 input token——坏掉的缓存最先在那里现形。

_用法：_

"长 session 的费用很凶——一次重构八美元。"

"查 cache token。如果 harness 在各 turn 之间重排 system prompt 或文件，前缀就断了，每个请求都按输入全价重付。"
