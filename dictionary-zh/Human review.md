---
description: 用户阅读 agent 产出的代码并作出判断。读 diff 算审查，读摘要不算。
---

用户阅读 [agent（智能体）](./Agent.md) 产出的代码并对其作出判断。读 diff 或改动过的文件算审查；读 agent 对自己所做之事的_描述_不算——叙述不是工件。描述是 [secondary source（二手来源）](./Secondary%20source.md)，由被审查的一方写成；diff 是 [primary source（一手来源）](./Primary%20source.md)，审查就是读它。

Agent 抬高了代码产量，于是审查成了瓶颈。一个有用的做法是分层叠加不同的审查策略。[Automated check（自动化检查）](./Automated%20check.md) 抓机械性失败，[automated review（自动化审查）](./Automated%20review.md) 抓可描述的失败，human review（人工评审）留给只有你能判断的东西——这个改动是不是对的改动、这个路子是否贴合代码库、这东西该不该存在。

审查也越早越便宜。开工前读一份计划，或飞行途中读一个小 diff，要几分钟；一次 [AFK](./AFK.md) 运行结束后刨一个完成的分支，要久得多。把审查检查点放在哪里，是一个 [human-in-the-loop（人在回路）](./Human-in-the-loop.md) 决定，不是事后补想。

_避免：_ 单说「code review」——分不清是人工还是自动。

_用法：_

「我人工审查了 AFK 的产出。」

「你读了 diff，还是只读了摘要？」

「Diff。摘要说它删了死代码——结果那函数从一个生成文件里被调用。」
