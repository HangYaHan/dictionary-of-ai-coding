---
description: 打包成单元的可教能力——留在 context window 外，直到 context pointer 为当前任务把它拉进来。
---

打包成单元的可教能力——把做好一件任务的指令和资源放在一起，留在 [environment（环境）](./Environment.md) 里，直到 [context pointer（上下文指针）](./Context%20pointer.md) 为当前任务把它拉进 [context window（上下文窗口）](./Context%20window.md)。这是 [harness（运行框架）](./Harness.md) 中 [progressive disclosure（渐进式披露）](./Progressive%20disclosure.md) 的单元。

Skill（技能）是开放标准，定义在 [agentskills.io](https://agentskills.io)——最初由 Anthropic 开发，此后被大多数主流 harness 采用，所以写一次的技能在各处可用。格式是一个文件夹，包含：

- 一个 `SKILL.md` 文件——元数据（至少一个名字和描述）加上指令本身
- 可选：[agent（智能体）](./Agent.md) 可运行的脚本
- 可选：指令所指向的模板和参考材料

默认只有名字和描述坐在 [context（上下文）](./Context.md) 里。Agent 的任务匹配时，才载入其余。在那之前，技能几乎不占地方——一两句 [token（词元）](./Token.md)，无论其完整指令有多大。

这把技能与 [AGENTS.md](./AGENTS.md.md) 区分开：后者不论任务都载入每个 [session（会话）](./Session.md)。技能是在特定一类工作出现时才读——发版、为新服务搭脚手架、写迁移——其余时候忽略。

_避免：_ "[tool（工具）](./Tool.md)"——tool 是 agent 调用的东西；skill 是它阅读的指令。

_用法：_

"部署手册该放哪？"

"作为技能——agent 只在任务涉及部署时载入它。放 AGENTS.md 里，会为我们每周才用一次的东西每 [turn（轮次）](./Turn.md) 都烧 token。"
