---
description: "model 周围把 model 变成 agent 的一切：tools、system prompt、context window 管理、permissions、hooks。"
---

围绕 [model（模型）](./Model.md)、把它变成 [agent（智能体）](./Agent.md) 的一切：[tools（工具）](./Tool.md)、[system prompt（系统提示词）](./System%20prompt.md)、[context window（上下文窗口）](./Context%20window.md) 管理、permissions（权限）、hooks（钩子）。**Claude.ai** 与 **Claude Code** 跑在同一个 model 上，行为却不同，因为它们的 harness（运行框架）不同。

Model 本身只做一件事：吃进文本，吐出文本。它读不了文件、跑不了命令、记不住上一个 [turn](./Turn.md)。这些全由 harness 提供。Harness 为每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 组装 [context](./Context.md)，执行 model 要求的 [tool call（工具调用）](./Tool%20call.md)，把 [tool result（工具结果）](./Tool%20result.md) 喂回去，存储 [session（会话）](./Session.md) 历史，在危险动作前向你要 permissions，并决定何时 [compact（压缩）](./Compaction.md)。Agent 循环——model 提议、harness 执行、重复——由 harness 驱动。

这一点对排查很重要。当两个产品之间、或昨天与今天之间行为不同时，变量往往不是 model，而是 harness。不同的 system prompt、不同的工具集、变更的权限默认值、新的 context 管理策略，都能在 model 毫无改动的情况下改变行为。这也意味着你的大部分配置都住在 harness 里：[AGENTS.md](./AGENTS.md.md) 文件、权限设置、hooks，全是指令 harness 的，不是指令 model 的。

例子：Claude Code、Cursor、Codex CLI——以及 Claude.ai，它是一个聊天 harness 而非编码 harness。

_用法：_

「同一个 model，为什么 Claude Code 在改文件，Claude.ai 只回答问题？」

「harness 不同——Claude Code 有 [filesystem（文件系统）](./Filesystem.md) 工具、不同的 system prompt 和一层 permissions。这里的变量不是 model。」
