---
description: 从 harness 到 model provider 的一次往返。harness 发送 context，provider 返回一次响应。
---

从 [harness（运行框架）](./Harness.md) 到 [model provider（模型提供商）](./Model%20provider.md) 的一次往返。harness 发送当前 [context（上下文）](./Context.md)；provider 返回一次响应（一个 [tool call（工具调用）](./Tool%20call.md) 或一个最终答案）。一条用户消息若让 [agent（智能体）](./Agent.md) 调用 [tool（工具）](./Tool.md)，可以触发多次 model provider request（模型提供商请求）——每个 [tool result（工具结果）](./Tool%20result.md) 都会再触发一次请求。

每次请求携带全部内容：[system prompt（系统提示词）](./System%20prompt.md)、到目前为止的完整对话、每条 tool result。[model（模型）](./Model.md) 是 [stateless（无状态）](./Stateless.md) 的，所以 provider 在请求之间不留任何东西——第 40 次请求重发第 39 次发过的全部内容，外加一条新的 tool result。[prefix cache（前缀缓存）](./Prefix%20cache.md) 就是为了让这种重复开销可以承受。

请求也是计费单位。[Input tokens（输入词元）](./Input%20tokens.md)、[output tokens（输出词元）](./Output%20tokens.md) 和缓存折扣都按请求统计，所以一个看起来无害的问题可能花费惊人：成本不正比于你的那条消息，而正比于请求数乘以每次请求携带的 context 大小。

值得把请求与 [turn（轮次）](./Turn.md) 区分开。turn 是与你的一次往来，而单个 turn——"修好失败的测试"——会展开成一串请求：

| 请求 | 模型返回                     | harness 随后                        |
| ---- | ---------------------------- | ----------------------------------- |
| 1    | tool call：跑测试            | 运行，追加失败输出                  |
| 2    | tool call：读测试文件        | 追加文件内容                        |
| 3    | tool call：读源文件          | 追加文件内容                        |
| 4    | tool call：编辑源文件        | 应用编辑，追加结果                  |
| 5    | tool call：再跑测试          | 运行，追加通过输出                  |
| 6    | 最终答案："修好了，测试通过" | 展示给你                            |

一个 turn 六次请求——每次都重发整个 context。当你疑惑 [token（词元）](./Token.md) 花到哪去了，数请求，别数 turn。

_用法：_

"一个问题烧了四万 token？"

"看 tool call——十二次 grep，八次 read，四次编辑。每个 tool result 都再起一次 model provider request，整个 [session（会话）](./Session.md) 前缀每次都重发。"
