---
description: harness 在每次 model provider request 发送的 tokens。费率低于 output tokens。
---

[Harness（运行框架）](./Harness.md) 在每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 上发送的 [tokens](./Token.md)——[system prompt（系统提示词）](./System%20prompt.md)、对话历史、[tool result（工具结果）](./Tool%20result.md)，以及 [model（模型）](./Model.md) 在落笔前读到的一切。计费费率低于 [output tokens](./Output%20tokens.md)，因为处理它们比处理输出 tokens 便宜。

做 [AI](./AI.md) 编程时，input tokens（输入 tokens）占账单的大头。Model 是 [stateless（无状态）](./Stateless.md) 的，所以每个 [turn（轮次）](./Turn.md) 都把整个 [session（会话）](./Session.md) 作为输入重发一遍：你的第一条消息、每个回复、此后每个 tool result。第五十轮的输入包含前四十九轮。一次 model provider request 可能只产出几百个输出 tokens，却重发十万 input tokens 的累积历史。第一轮便宜，越往后越贵——每一轮都背着之前所有轮，而其中最大块常常是 tool result：一次读文件或命令输出就能加几千 tokens，且此后每轮重发。

[Prefix cache（前缀缓存）](./Prefix%20cache.md) 降低这笔开销：与之前某次请求完全一致的历史，按便宜的 [cache token（缓存 tokens）](./Cache%20tokens.md) 计费，而非全价输入。当输入成本仍然痛时，修法是缩小被重发的内容——在任务之间 [clearing（清空）](./Clearing.md) 或 [compacting（压缩）](./Compaction.md)。

_用法：_

「账单很高，但 [agent](./Agent.md) 几乎没写出什么东西。」

「是 input tokens——每个 turn 重发整个 session。没有 prefix cache，你每次请求都在为历史重新付钱。」
