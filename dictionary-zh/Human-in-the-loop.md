---
description: 一种工作模式：一个或多个人在 session 中与 agent 结对——实时审查、转向或协作。
aliases:
  - HITL
  - Human-in-the-loop (HITL)
---

一种工作模式：一个或多个人在 [session（会话）](./Session.md) 期间与 [agent（智能体）](./Agent.md) 结对——实时审查、转向或协作。人是在场且投入的，不只是给单个动作放行。

对照的是 [AFK](./AFK.md) 工作：agent 无人值守地跑，你事后评判结果。Human-in-the-loop（人在回路，HITL）意味着在问题还便宜的时候抓住它：你看见 agent 去够错误的文件、误读了需求、或走上一条死路，用一句话把它拉回来——而不是在二十分钟自信的工作建立在那个错误之上才发现。Agent 并不能可靠地知道自己偏了轨；没人管时，它们倾向于继续往前推，而不是停下提问。

哪种模式合适取决于工作本身。规格清楚、风险低、易验证的任务适合 AFK。模糊、不可逆、或你难以审查成品的任务——一次 schema 迁移、一个棘手的设计决定、任何碰生产环境的东西——适合留在回路里。这个判断本质上是：一次走错代价多大，你要多久才会发现？

有些工作天生就是 in-the-loop，因为你的反应就是输入。[Grilling](./Grilling.md) 只有你在场回答问题才成立；[prototyping（原型制作）](./Prototyping.md) 只有你在场对工件作出反应才成立。

留在回路里消耗你的注意力，而注意力是稀缺资源。用好 agent 的一部分，是把更多工作安全地移出回路——用计划、[automated check（自动化检查）](./Automated%20check.md)，以及结尾处的 [human review（人工评审）](./Human%20review.md)，代替全程监督。

_用法：_

「这个 AFK 跑一夜？」

「不，schema 迁移——保持 human-in-the-loop。我要看到每一步，如果它挑错了回填所用的列，我要能转向。」
