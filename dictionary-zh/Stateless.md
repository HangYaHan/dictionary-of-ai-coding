---
description: 不向前携带信息。model 跨请求无状态；agent 默认跨 session 无状态。
---

不向前携带信息。[Model（模型）](./Model.md) 跨 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 无状态——每次请求重发整个 [context window（上下文窗口）](./Context%20window.md)，因为模型没有别的途径看到任何东西。[Agent（智能体）](./Agent.md) 默认跨 [session（会话）](./Session.md) 无状态：新 session 从空开始，没有旧 session 的任何痕迹。与 [stateful（有状态）](./Stateful.md) 相对。

模型本身永久无状态：它的 [parameters（参数）](./Parameters.md) 在 [training（训练）](./Training.md) 后冻结，[inference（推理）](./Inference.md) 期间你做什么都改不了它们。模型不从你的纠正中学习，不记得昨天被告诉过同一件事，也不是在逐渐了解你——无论对话感觉多像那样。Session 内的连续感由 [harness（运行框架）](./Harness.md) 制造：它保存 transcript（对话记录），每次请求重发。模型不是在记得对话；它是在重读对话。

实际后果：想让某样东西跨 session 被记住，就必须写到 agent 会读回来的地方。[AGENTS.md](./AGENTS.md.md) 文件、[memory system（记忆系统）](./Memory%20system.md)、[handoff artifact（交接产物）](./Handoff%20artifact.md) 就是干这个的——载入未来 session 的 [context（上下文）](./Context.md)，替模型补上它没有的记忆。当 agent 反复犯你纠正过的错，问题不是它为何没学会——它学不会——而是那条纠正该写在哪，好让每个未来 session 都读到它。

_用法：_

"为什么每次我 [clear（清空）](./Clearing.md) 它都忘掉那条约定？"

"模型无状态——新 session 从空开始。想让它带上，就写进 AGENTS.md 或 harness 在 session 开头加载的记忆文件。"
