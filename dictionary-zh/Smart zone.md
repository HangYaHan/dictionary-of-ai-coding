---
description: "session 早期 agent 锐利专注。session 变长后漂入愚钝区：更草率、更健忘、更多错误。"
aliases:
  - Dumb zone
  - Smart zone / Dumb zone
---

[Session（会话）](./Session.md) 早期，[agent（智能体）](./Agent.md) 处在 smart zone（智能区）——锐利、专注、回忆良好。Session 变长，它漂进 dumb zone（愚钝区）：更草率、更健忘、更多错误——以及更"忠实"的 [hallucination（幻觉）](./Hallucination.md)。同一个 [model（模型）](./Model.md)、同一个 [harness（运行框架）](./Harness.md)——只是 [context（上下文）](./Context.md) 更多。这是 [attention degradation（注意力衰减）](./Attention%20degradation.md) 的可感效果。在前沿模型上，愚钝区通常始于 125K-150K [token（词元）](./Token.md) 左右——不过这有争议。[Clear（清空）](./Clearing.md) 或 [compact（压缩）](./Compaction.md) 当 session 膨胀；别硬撑。

衰退是渐进的，因此容易漏掉。没有错误消息，也没有可见边界；agent 只是开始表现略差，然后明显更差。常见征兆：忘了你二十轮前给的指令、重复它已纠正过的错误、或自信断言 context 所否定的东西。因为滑坡平滑，通常反应是硬撑并再解释一遍——这加入更多 context，让问题更糟。

这些区不跟着 [context window（上下文窗口）](./Context%20window.md) 上限走。Session 可以深陷愚钝区而窗口大半还空着：上限是 harness 拒绝继续之处，而质量早在那之前就掉了。围绕智能区做计划，不是围绕窗口——一项任务的实际预算是 agent 在其中工作良好的 token 数，不是它技术上装得下的 token 数。

智能区是预算，不相干的工作会花掉它。Session 里做的每个任务都耗用 token，所以在同一 session 开第二个任务，意味着离愚钝区更近地开始它。一个 session 一个任务，让每个任务拿到 session 最锐利的部分。当单个任务大过一个智能区，就拆开：在自然边界 [hand off（交接）](./Handoff.md) 或压缩，让新 session 做下一段。

_用法：_

"前三个组件都拿下了，第四个砍得稀烂。"

"你出了智能区——同一个 model，只是已深入愚钝区。压缩并重新载入计划，下一个组件会成。"
