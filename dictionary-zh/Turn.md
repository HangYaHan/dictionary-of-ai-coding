---
description: 一条用户消息加上 agent 为其响应所做的一切，直到交还控制权。包含一次或多次 provider request。
---

一条用户消息加上 [agent](./Agent.md) 为响应它所做的一切，直到 agent 把控制权交还用户。包含一次或多次 [model provider request](./Model%20provider%20request.md)——agent 调用 [tool](./Tool.md) 时就是多次。一个澄清问题关闭当前 turn；你的回复开启下一个。层级是 [session](./Session.md) **> Turn > Model provider request**。

Turn（轮次）值得命名的原因是：它的长度由 agent 决定，不由你决定。你交出一条消息；agent 决定在交还之前串联多少次 tool call。一个 turn 可以是一句话的回答，也可以是二十分钟的阅读、编辑和跑测试。这是同一属性的两个视角：长 turn 使 [AFK](./AFK.md) 工作成为可能；长 turn 也是无人监督下出问题的地方——到 agent 交还时，它可能已经偏离你的本意很远。

Turn 也是引导的自然单位。turn 内部的一切都在没有你的情况下发生；turn 之间的间隙才是你转向方向的地方。多数 [harness](./Harness.md) 缓和了这一点：你可以在 turn 中途打断以停止并引导 agent，或在它工作时输入一条消息，该消息在 turn 完成后被读取。如果你发现自己反复不满 turn 的最终走向，解法通常是要求更小的 turn——先要计划、一次一步——用自主性换取更频繁的可引导间隙。

_用法：_

「一个 turn 花了两分钟？」

「它在那个 turn 里做了十四次 [tool call](./Tool%20call.md)——每次都是单独一次 model provider request。在 agent 最终交还给你之前，延迟层层叠加。」
