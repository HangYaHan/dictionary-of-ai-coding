---
description: harness 在每次 model provider request 前附加的指令——agent 的常设任务书。通常在整个 session 内保持稳定。
---

[harness](./Harness.md) 在每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md)前附加的指令——[agent](./Agent.md) 的常设任务书：它是谁、如何行为、可调用哪些 [tool](./Tool.md)、遵循哪些约定。通常在整个 [session](./Session.md) 内保持稳定。

System prompt（系统提示词）由 harness 厂商撰写，不是你写的，而且在编码类 harness 里篇幅很大——往往是数万 [token](./Token.md) 的行为规则、工具描述和边界情况处理，每个 [turn](./Turn.md) 都作为 [input tokens（输入 token）](./Input%20tokens.md)计费。你自己的常设指令也搭在其中：[AGENTS.md](./AGENTS.md.md) 这类文件在 session 开始时与 system prompt 并列加载，所以 [model](./Model.md) 在见到你的消息之前，先一起读了厂商的任务书和你的任务书。

因为每次请求中它完全相同，它构成 [prefix cache（前缀缓存）](./Prefix%20cache.md)的开头——这也是 harness 整个 session 固定它、而不边跑边改的原因之一。

模型受训练为让 system prompt 优先于用户消息。所以当 agent 坚持某个你从未要求的约定，或用你改不动的方式格式化输出时，它通常是在服从自己的 system prompt——你的消息在这场争论里输了。有些 harness 可定制：给你 system prompt 的完全访问权限，你可以读到 agent 实际被交代了什么并加以修改。

_用法：_

「两个 harness，同一个模型，同一提示词，行为完全不同。」

「system prompt 不同。一个调成简短代码编辑，另一个调成解释说明——分歧在这里，还没轮到你的消息。」
