---
description: Agent experience：环境为 agent 干好活铺垫得如何——检查、架构和空余 context。
aliases:
  - Agent experience
---

Agent experience——[environment](./Environment.md) 为 [agent](./Agent.md) 在 codebase 里干好活铺垫得如何。面向 agent 的、对应 [DX](./DX.md) 的一面。同一个 agent 在一个仓库表现好、在另一个差——同一个 [model](./Model.md)，同一个 [harness](./Harness.md)——差别通常是 AX。直觉是怪 model 或重写 prompt；修复更多在仓库里。

好的 AX 有三个主要维度：

| 维度            | 好的 AX 长什么样                                                                                                                                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 自动化检查（Automated checks） | 快速、确定的 [automated checks](./Automated%20check.md)——类型、测试、lint——agent 无须人就能据以自纠                                                                                 |
| 架构（Architecture）     | agent 无须通读即可导航的 codebase：可预测的结构、大量行为藏在小接口后面、名字说明用途                                                                                               |
| 空余 context（Free context）     | [AGENTS.md](./AGENTS.md.md)、[skills](./Skill.md) 和 [tools](./Tool.md) 保持精简，使大部分 [context window](./Context%20window.md) 可用于任务，agent 留在 [smart zone](./Smart%20zone.md) 而非溺水                                   |

AX 与 DX 重叠——好的检查和干净的架构对双方受众都有帮助——但它们分岔。人能忍受部落知识、慢 CI、和"计费模块问 Sarah"；agent 不能。Agent 不受益于 IDE 提示或漂亮仪表盘；它们要的是作为文本出现在 [tool result](./Tool%20result.md) 里的失败。一个 codebase 可以有好 DX 和差 AX。

_避免：_把 AX 当 DX 同义词——两个受众需要不同的投入。

_用法：_

"agent 在 API 仓库写好代码，在前端写垃圾。"

"API 仓库类型严格、测试套件快；前端两样都没有外加四十个总是加载的 skill。那是 AX 差距，不是 model 问题。"
