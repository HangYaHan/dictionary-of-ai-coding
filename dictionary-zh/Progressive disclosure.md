---
description: 只载入 agent 此刻需要的 context，其余用 context pointer 指路。借自 UI 设计。
---

只载入[agent](./Agent.md)（智能体）此刻需要的[context](./Context.md)（上下文），其余用[context pointer](./Context%20pointer.md)（上下文指针）指向。借自 UI 设计：那里指只向用户展示与当前任务相关的控件，其余藏在一个点击之后。

这技术存在，因为 context 成本是双重的。每个前置载入的[token](./Token.md)（词元），每[turn](./Turn.md)（轮次）都按[input tokens](./Input%20tokens.md)（输入 token）计费，且每个 token 都消耗[attention budget](./Attention%20budget.md)（注意力预算），不管 agent 是否需要。塞满完整风格指南、部署手册和数据库约定的[AGENTS.md](./AGENTS.md.md)，会让 agent 在所有这些事情上都更差——对当前任务要紧的指令被不要紧的稀释了。征兆是 agent 忽略你明知在它 context 里的规则：规则在，但被埋了。

progressive disclosure（渐进式披露）反过来做。把常载层保持很小——每个主题一句话，加一个细节所在处的指针。agent 写组件时读风格指南，部署时读部署手册，修测试时两者都不读。[Skills](./Skill.md)（技能）就是[harness](./Harness.md)（运行框架）内建的这一模式：每次[session](./Session.md)（会话）载入一段简短描述，完整指令只在触发时载入。

_用法：_

"要不要把整个风格指南倒进 AGENTS.md？"

"不要——用 progressive disclosure。把风格指南作为 skill 引用，agent 真要写组件时再载入它。AGENTS.md 每 turn 都付 token 成本。"
