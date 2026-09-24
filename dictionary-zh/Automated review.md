---
description: 一个 agent 审查另一个 agent 的工作，常用不同 model 或 system prompt。非确定性：它形成判断。
---

一个 [agent](./Agent.md) 审查另一个 agent 的工作，常用不同的 [model](./Model.md) 或 [system prompt](./System%20prompt.md)。非确定性：它形成判断。可运行于任何地方——PR 合并前、提交历史事后、会话中途作为 [subagent](./Subagent.md)。CI 里的 LLM-as-judge 是 automated review，不是 [automated check](./Automated%20check.md)；断言 _做什么_ 决定类别，不是在哪跑。

与工作 agent 的分离是它奏效的原因。让写代码的 agent 审自己的工作，收获很少——产生 bug 的 [session](./Session.md) 也包含产生它的推理，agent 把自己的结论读回来当确认。拥有新鲜 [context window](./Context%20window.md) 的审查者没有那种依恋：它像陌生人一样看 diff，而 review 依赖的正是这一点。不同 model 或审查专用 system prompt 进一步锐化它——不同的盲区，以及 scoped 到你真正关心的（安全、API 契约、性能）的 system prompt，而非含糊的"找找问题"。

它嵌在其他 review 层之间。Automated checks 是确定的，捕捉可机械断言的；[human review](./Human%20review.md) 昂贵且扩展性最差。Automated review 居中：它以机器成本捕捉判断形状的问题——一个误导性的函数名、一个漏掉的边缘情况。因为它非确定性，它会漏事、会误报；把它当作人看之前抬高底线的过滤器，不是取代人的闸。

_避免：_"AI review" / "agent review"——太含糊，无法与工作 agent 本身区分。

_用法：_

"[AFK](./AFK.md) 运行给出的坏 PR 太多了。"

"合并前加一个 automated review 步骤——不同 model，独立 system prompt，scope 到安全和契约变更。"
