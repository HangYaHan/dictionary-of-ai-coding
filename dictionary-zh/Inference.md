---
description: 运行训练好的 model 生成输出——每次 model provider request 发生的事。parameters 保持固定。
---

运行训练好的 [model（模型）](./Model.md) 以生成输出——每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 发生的事。[Parameters（参数）](./Parameters.md) 保持固定；model 只是就给定的 [context（上下文）](./Context.md) 做 [next-token prediction（下一 token 预测）](./Next-token%20prediction.md)。相对 [training（训练）](./Training.md) 便宜，但按 [token](./Token.md) 计费，是使用 model 的主导成本。

Model 的一生分为两个阶段：

| 阶段 | 何时发生 | 做什么 | parameters |
| ---- | -------- | ------ | ---------- |
| Training | 一次，在发布前 | 从训练语料产出 parameters | 被写入 |
| Inference（推理） | 每当任何人使用 model | 把冻结的 parameters 跑过你的 context 生成 tokens | 只读 |

推理阶段你做的任何事都不会写回 parameters——这就是你今天的纠正到明天不起作用的原因。下一个 [session（会话）](./Session.md) 里 model 犯同样的错，尽管你仔细解释过修法：它不是无视你，而是无力从那次交流中学习。Model 是 [stateless（无状态）](./Stateless.md) 的——连续性必须来自外部——来自 [context window（上下文窗口）](./Context%20window.md) 或 [memory system（记忆系统）](./Memory%20system.md)。

这一机制也解释了计费方式。每次请求都把 model 跑过完整 context，所以成本随 [input tokens（输入 tokens）](./Input%20tokens.md) 和 [output tokens（输出 tokens）](./Output%20tokens.md) 增长，一个做几十次 [tool（工具）](./Tool.md) 调用的 agent 每个往返都付推理费。这就是为什么 context 大小既是质量问题也是成本问题。

_用法：_

「为什么账单随用量走，而不是一个固定授权价？」

「你付的是 inference——每次 model provider request 都在提供方的硬件上跑 model。训练已经发生过了，但推理成本按请求累积，而且当工具被调用时，单个 [turn（轮次）](./Turn.md) 能扩展成许多次请求。」
