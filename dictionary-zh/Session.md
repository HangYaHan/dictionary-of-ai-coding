---
description: 与 agent 的一段有界交互。从空开始累积，清空、关闭或压入新会话时结束。
---

与 [agent（智能体）](./Agent.md) 的一段有界交互。从空开始，累积消息、[tool result（工具结果）](./Tool%20result.md) 和读过的文件，在被 [cleared（清空）](./Clearing.md)、关闭，或 [compacted（压缩）](./Compaction.md) 进新 session 时结束。Session 就是填满 [context window（上下文窗口）](./Context%20window.md) 的东西：如果 context window 是盒子，session 就是慢慢把它装满的物件。大到一个 context window 装不下的工作必须拆到多个 session。

Session 的消息历史就是 agent 的工作记忆。[Model（模型）](./Model.md) 是 [stateless（无状态）](./Stateless.md) 的，所以它看似记得的一切——你要什么、测试说了什么、三轮前它决定了什么——都在消息历史里，随每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 重发。不在 session 里的东西，对 agent 而言不存在。

这份记忆随 session 终结。新 session 从零开始：昨天 session 末尾还很懂你代码库的 agent，今早什么都不懂。活下来的是 [filesystem（文件系统）](./Filesystem.md)——一个 session 期间写的文件能被下一个 session 读到，[handoff（交接）](./Handoff.md)、[memory system（记忆系统）](./Memory%20system.md) 和 [AGENTS.md](./AGENTS.md.md) 都靠这个。

Session 在哪里结束由你选。Session 里的一切影响之后每个 [turn（轮次）](./Turn.md)，所以在一个 session 里做不相干任务会留下残渣，给下一个回答染色。一个 session 一个任务让 context 保持切题；完成任务是自然的清除点。

_用法：_

"一个 session 能跑多久才散架？"

"看工作——聚焦的重构比开放式研究撑得久。session 膨胀了就交接或压缩，别硬撑。"
