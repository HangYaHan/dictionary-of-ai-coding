---
description: 让 agent 跨会话保持状态的系统：会话中持久化到环境，下次会话开始时重新加载。
---

一种让 [agent（智能体）](./Agent.md) 跨 [session（会话）](./Session.md) 保持 [stateful（有状态）](./Stateful.md) 的系统。会话期间把信息写入 [environment（环境）](./Environment.md)，未来会话开始时再加载回 [context window（上下文窗口）](./Context%20window.md)，使 agent 在用户 [clearing（清空）](./Clearing.md) 会话之后仍保有连续性。

memory system（记忆系统）分两半。写路径：会话中，agent 把学到的东西——你说过的偏好、关于项目的事实——记成环境里的文件。读路径：会话开始时，[harness（运行框架）](./Harness.md) 把这些文件或其索引加载回 context window。许多 harness 自带 memory system——Claude Code 的 `/memory` 就是一个——你也可以自己搭：一个笔记目录，外加 [AGENTS.md](./AGENTS.md.md) 里一条查阅它的指令。

任何常驻加载内容的取舍都适用。记忆会累积，所以多数系统只加载一行索引，正文留在 [context pointer（上下文指针）](./Context%20pointer.md) 后面，而不是全部内联。而且记忆是 [secondary source（二手来源）](./Secondary%20source.md)，会漂移：三月记下的事实，六月在项目已改样之后仍以同等置信度加载。memory system 需要修剪，和 AGENTS.md 一样。

_用法：_

"我老得反复告诉它我用 Postgres，不是 MySQL。"

"接一套 memory system——第一个 [turn（轮次）](./Turn.md) 就把学到的写到 [filesystem（文件系统）](./Filesystem.md)，下次会话开始时重新加载。[model（模型）](./Model.md) 本身是 [stateless（无状态）](./Stateless.md)；记忆层伪造连续性。"
