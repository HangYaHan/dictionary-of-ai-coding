---
description: context window 接近满时，由 harness 自动触发的 compaction。
---

[Compaction](./Compaction.md)，由 [harness](./Harness.md) 在 [context window](./Context%20window.md) 接近满时自动触发。

harness 监视 context window 有多满。越过阈值——常在 80% 左右——它暂停，请 [model](./Model.md) 总结迄今为止的 [session](./Session.md)，并以该总结播种一个新会话。然后工作像什么都没发生一样继续。

但确实发生了什么。Compaction 是有损的，autocompact 在你未选择的时刻有损。手动 compact 发生在阶段边界，你能告诉 model 保什么。Autocompact 在任务中途触发，阈值一到就打——可能在重构做了一半时，由总结自行决定你的哪些决策值得保留。典型症状：[agent](./Agent.md) 继续自信推进，却悄悄忘记了一小时前确立的某个约束，直到其工作开始与之矛盾你才注意到。

防御是不让它触发。监视 context 指示器，在自然边界手动 compact，或把决策写进盘上的计划文档或 [handoff artifact](./Handoff%20artifact.md)，总结丢不掉它们。多数 harness 也允许自定义缓冲——把阈值调前或调后，或干脆关掉 autocompact——这样你能调触发前保留多少余量。

_用法：_

"它好像不记得我们早先关于 schema 的决定了。"

"Autocompact 在 [turns](./Turn.md) 之间触发了——早期决策被总结掉了，肯定丢了东西。重载计划文档，或下次手动 compact，由你控制保什么。"
