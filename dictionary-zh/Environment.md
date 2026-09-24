---
description: agent 作用于其中的世界——harness 之外，agent 经 tool result 感知、经 tool call 改变的一切。
---

environment（环境）是 [agent](./Agent.md)（智能体）作用于其中的世界——[harness](./Harness.md)（运行框架）之外、agent 经 [tool results](./Tool%20result.md)（工具结果）感知、经 [tool calls](./Tool%20call.md)（工具调用）改变的一切。harness_运行_ agent；环境是 agent_工作于其中_的地方。像 [`AGENTS.md`](./AGENTS.md.md) 这样的文件活在环境里；把它载入 [context window](./Context%20window.md)（上下文窗口）的是 harness。[filesystem](./Filesystem.md)（文件系统）是最常见的环境种类，但不是唯一的（数据库、远程 API、浏览器 session（会话）都可以是环境）。

agent 只在看的时候才看见环境。它对环境所知的一切都经 tool result 到达，所以它的图景是一叠快照，每张在拍下那一刻准确。文件在 agent 读过之后变了——你手动编辑了它、构建步骤重新生成了它——agent 会继续基于过期的副本推理，直到某件事促使它重读。agent 自信地描述一个已不再如此的文件，通常是这种情况：环境动了，快照没动。

环境也是持久的那一层——唯一永远 [stateful](./Stateful.md)（有状态）的一层。[session](./Session.md)的 context（上下文）随 session 结束而消失，但写进环境的文件留着给下一个 session 读——[memory systems](./Memory%20system.md)（记忆系统）、[handoff artifacts](./Handoff%20artifact.md)（交接产物）和 `AGENTS.md` 靠的正是这个。agent 明天仍该知道的任何东西，都必须最终落在环境里。

环境多大由你决定。[sandbox](./Sandbox.md)（沙箱）缩小它，限制 agent 能触及什么；加一个 [tool](./Tool.md)（工具）扩展它，把数据库或 API 带进可达范围。边界内的，是 agent 能感知和改变的；边界外的一切对 agent 不存在。环境为支撑 agent 的工作铺垫得如何，就是代码库的 [AX](./AX.md)。

_避免：_用 "environment" 指运行时或 harness 本身——harness 是外壳，环境是工作区。

_用法：_

"agent 看不到 staging DB 的 schema。"

"把它接进环境——给它一个限定在 staging 只读的 `psql` 工具。harness 没问题，它只是没有可作用的东西。"
