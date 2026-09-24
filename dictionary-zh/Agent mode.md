---
description: 一种预设，把 permission mode 与注入 system prompt 的行为指令打包在一起。可中途切换。
aliases:
  - plan mode
  - accept-edits
  - bypass permissions
  - YOLO mode
---

一种预设，塑造 [agent](./Agent.md) 在运行时如何行事——把 [permission mode](./Permission%20mode.md) 与注入 [system prompt](./System%20prompt.md) 的行为指令打包在一起。例子：默认模式对高风险调用弹确认，**plan mode** 阻止编辑、引导 agent 去研究，**accept-edits** 模式自动批准编辑，**bypass permissions** 模式（俗称 **YOLO mode**）自动批准一切。可以 [mid-session](./Session.md) 切换。

打包是模式区别于裸权限设置的地方。permission mode 只是一道闸：它决定哪些 [tool calls](./Tool%20call.md) 放行。只有闸，得到的是一个想编辑却不能的 agent——它提出写入，被拦，再换一条路。注入的指令移除了那个"想"：plan mode 不只阻止编辑，它告诉 agent 当前处于规划阶段，所以它去读、去问、去提议，而不是顶着闸硬来。闸和方向盘指向同一边。

实践中，你随任务推进中的信任变化而切换模式。同一任务会经过几个模式：方法还在成形时用 plan mode，最初几处精细编辑用弹确认的默认值，agent 表现出理解改动后用 accept-edits，为一次 [AFK](./AFK.md) 运行、在 [sandbox](./Sandbox.md) 内，用 bypass。切换模式没有代价：对话原地继续，只有权限和指令变新。如果你发现自己不经阅读就批准每个提示，模式设得比你实际信任紧；如果你不断驳回编辑，设得比实际信任松。

_Vendor terms:_ Claude Code 称之为 "permission modes"，Codex 称之为 "approval modes"——两者都早于行为打包。

_用法：_

"我只想要个计划，它却一直在改文件。"

"切到 plan mode——会挡住写入，停在研究阶段。"

"稍后那次 AFK 运行呢？"

"Bypass 模式，但只在 sandbox 里面。"
