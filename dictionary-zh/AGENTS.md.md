---
description: 环境中的一个文件，harness 在 session 开始时载入 context window——项目给 agent 的常备简报。
---

[Environment](./Environment.md) 中的一个文件，[harness](./Harness.md) 载入 [context window](./Context%20window.md)，时在 [session](./Session.md) 开始——项目给 [agent](./Agent.md) 的常备简报。跨 harness 惯例；有些 harness 还有自己的变体（Claude Code 的是 CLAUDE.md）。

因为它自动加载，所以是避免跨会话重复交代的一种方式。[model](./Model.md) 是 [stateless](./Stateless.md) 的——你在某会话给的纠正，下个会话就没了，于是你不得不对每个新会话重复：项目用 pnpm、测试带某个 flag 跑、某目录是生成的别碰。当你为同一件事纠正 agent 两次，那条纠正就是 AGENTS.md 的候选行。

合适的内容是 agent 无法从代码推导的东西：构建和测试命令、代码库没有明说的惯例、硬约束（"永远不改生成的 client"）。短而陈述式——这是简报，不是文档。

代价是里面的一切总是被加载。指令不断累积，多数与任何给定任务无关，而长 AGENTS.md 既花 token 又稀释自己——context 里指令越多，model 遵守任何一条的可靠性越低。

_避免：_把本该 [progressively disclosed](./Progressive%20disclosure.md) 的内容放进 AGENTS.md——里面任何一行都以 [token](./Token.md) 计价，每个 [turn](./Turn.md)、每个会话付一次，无论该会话是否需要。样式指南可以放到 [skill](./Skill.md) 或 [context pointer](./Context%20pointer.md) 后面；AGENTS.md 留给处处适用的行。

_用法：_

"为什么每个会话一上来就烧掉 4k token？"

"查 AGENTS.md——有人把整份样式指南贴进去了，本该放 skill 后面。"
