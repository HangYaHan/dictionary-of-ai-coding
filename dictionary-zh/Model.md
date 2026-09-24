---
description: 即 parameters。无状态——只做 next-token prediction，别无其他。自身无法做任何 agentic 行为。
---

就是 [parameters（参数）](./Parameters.md)。[stateless（无状态）](./Stateless.md)——只做 [next-token prediction（下一词元预测）](./Next-token%20prediction.md)，别无其他。"Claude Opus 4.x" 和 "GPT-5.x" 都是 model（模型）。模型单独做不了任何 agentic 行为；必须被 [harness（运行框架）](./Harness.md) 驱动。

模型不能读文件、跑命令、上网，也不能记住昨天——它吃进 [token（词元）](./Token.md) 吐出预测的 token，每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 一回。一切看起来像 [agent（智能体）](./Agent.md) 在干活的事——选 [tool（工具）](./Tool.md)、读结果、循环到任务完成——都是 harness 在编排一连串这样的预测。

[model provider（模型提供商）](./Model%20provider.md) 分层出货：一个最大最聪明但慢且贵的，加几个更快更便宜但能力弱的。选层是实际决策——规划和难缠的调试用重量级，机械改动用轻量级——harness 允许你在 [session（会话）](./Session.md) 中途切换。

严格用这个词也能让诊断更清楚。"模型不擅长这个" 是具体主张——同一个模型换一个 harness，或换一份 [context（上下文）](./Context.md)，表现常完全不同。怪模型之前先看给了它什么：多数令人失望的输出追溯回去是 context 或 harness 的问题，不是 parameters。

_用法：_

"规划步骤要不要把模型从 Sonnet 换成 Opus？"

"可以试——但这个任务大头是 harness 在扛。如果 [system prompt（系统提示词）](./System%20prompt.md) 和工具不对，换模型没用。"
