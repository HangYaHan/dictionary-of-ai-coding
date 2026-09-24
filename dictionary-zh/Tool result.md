---
description: harness 执行 tool call 后送回的内容——文件内容、输出或错误。agent 感知环境的唯一途径。
---

[harness](./Harness.md) 执行 [tool call](./Tool%20call.md) 后送回的内容——文件内容、命令输出、错误。[agent](./Agent.md) 感知 [environment（环境）](./Environment.md)的唯一途径。它在_下一个_ [model provider request](./Model%20provider%20request.md) 中回到 [model](./Model.md)，由模型决定如何处置。Tool call 和 tool result 是同一次交换的两端，都在一个 [turn](./Turn.md) 之内。

Tool result（工具结果）的生命周期：

| 步骤 | 谁 | 发生什么 |
| ---- | -- | -------- |
| 1 | Harness | 执行 tool call——运行命令、读取文件 |
| 2 | Harness | 捕获结果：输出、内容或错误 |
| 3 | Harness | 作为消息追加进 [context](./Context.md) |
| 4 | Harness | 在下一次 model provider request 中把整个 context 发给提供方 |
| 5 | 模型 | 读取结果并决定：再来一次 tool call，还是给出最终回答 |

结果在余下的 [session](./Session.md) 中一直留在 context 里。Tool result 通常占编码 session context 的大头：每次读文件、每次跑测试、每次搜索都完整落入，并在早已无用之后继续占用 [token](./Token.md)。少数大结果——冗长的测试日志、整篇读入的生成文件——能把 session 推向 [context window](./Context%20window.md) 边缘的速度比对话本身还快。

因为结果是模型看到的一切，模型无法核查其背后的环境。如果输出被截断、命令静默失败，或 harness 返回了错误而非内容，模型只能基于拿到的东西推理。当你觉得 agent 对系统的描绘不对时，该查的就是 tool result：transcript 某处有一条结果说的和你确知的事实不同。

_用法：_

「它推理这个文件的方式好像文件是空的。」

「Tool result 回来的是权限拒绝，不是内容。模型只看到错误字符串——它没有别的途径看到文件。」
