---
description: 一个被配上工具、system prompt 和 context window 的 model，与用户轮流交互。运动中的 model。
---

一个 [model](./Model.md)，[harnessed](./Harness.md) 上 [tools](./Tool.md)、[system prompt](./System%20prompt.md) 和 [context window](./Context%20window.md)，与用户轮流 [turns](./Turn.md)。_Claude Code 是 agent。Cursor 是 agent。Claude.ai 是 agent。_ 你实际对话的对象就是 agent——它是运动中的 model，为某个目的配置好的。

与本词典多数术语不同，"agent" 不指某个机械部件。model 是一份 [parameters](./Parameters.md)；harness 是你能指向的软件。agent 两者都不是——它是你正在对其说话的单元。人们不断把 [AI](./AI.md) 拟人化，而 agent 就是那个被拟人化的单元：你委托的对象，读你消息并回答的对象，"它又把构建搞坏了"里的那个"它"。你说 agent 做了某事，意思是 model 加 harness 做了它，但你把这组合当成单一行为者来称呼。

这个混称在排查时会挡路。说 "agent 写错了" 不区分是 model 输出错，还是 harness 侧的配置错——工具、权限、装进去的 context。定位要拆开：同一 harness 换 model 重跑，或同一 model 换 harness，看错误跟哪边走。

这个想法比这波 AI 更早。软件 agent——你把目标委托给它、它代你行事的程序——和 AI 本身一样古老。今天说 agent 多指 LLM 循环加工具的实现，委托-执行的结构没变。

_避免：_"the AI"、"the bot"（太含糊——掩盖了你指 parameters 还是被 harness 的那个东西）。

_用法：_

"迁移你用哪个 agent？"

"本地 Claude Code，UI 部分用 Cursor——底下同一个 model，不同 harness。"
