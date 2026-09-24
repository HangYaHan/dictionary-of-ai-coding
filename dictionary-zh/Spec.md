---
description: 描述多会话工作的交接产物——做什么建什么，不管每个会话怎么做那份。由工单构成。
---

A [handoff artifact（交接产物）](./Handoff%20artifact.md)，描述一段跨多 [session（会话）](./Session.md) 的工作——要建什么，不管每个 session 怎么做自己那份。随工作推进而变动。由 [ticket（工单）](./Ticket.md) 构成。

Spec（规格说明）存在，因为 session 用完即弃而大工作不是。任何需要超过一个 [context window（上下文窗口）](./Context%20window.md) 工作量的事，都需要一个在 [context（上下文）](./Context.md) 之外的家——[environment（环境）](./Environment.md) 里能挺过 [clearing（清空）](./Clearing.md) 的地方，无论那是仓库里的一个文件、一个 GitHub issue，还是 agent 够得着的问题追踪器。Spec 就是那个家：目标、约束、迄今做出的决定，以及带状态的工单列表。任何新 session 都能读它、知道工作进展到哪，而不必继承上一个 session 累积的噪声。

Spec 有几种可辨认的样式，多半沿袭团队已经记东西的方式。_产品需求文档_（PRD）偏面向用户的 what 和 why——功能、行为、验收标准。_设计文档_ 或 _RFC_ 偏技术——选定的方案、被否的替代、权衡。小的一端，一个朴素的 `PLAN.md` 加一张工单清单，对多 session 功能干同样的活。样式不如角色重要：对 [agent（智能体）](./Agent.md)，这些都是同一样东西——每个 session 开头它读的、持久的意图陈述。

_用法：_

"这些全该在一个 session 里做吗？"

"不，写成 spec——拆成工单，每个工单跑自己的 session。想在一个 context 里做完全部，不到一半就会撞上 [dumb zone（愚钝区）](./Smart%20zone.md)。"
