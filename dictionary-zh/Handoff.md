---
description: 把 agent context 从一个 session 转移到另一个，无返回路径。载体各异——artifact、compaction 等。
---

把 [agent（智能体）](./Agent.md) 的 [context（上下文）](./Context.md) 从一个 [session（会话）](./Session.md) 转移到另一个。载体各异——一份写下的 [handoff artifact（交接工件）](./Handoff%20artifact.md)、一份内存中的摘要（[compaction（压缩）](./Compaction.md)），以及其他方式。与 [clearing（清空）](./Clearing.md) 不同（后者根本不转移）。理由各异：切换角色（规划者 → 实现者）、发起一次 [AFK](./AFK.md) 运行、扇出到并行 session，或腾出 [context window（上下文窗口）](./Context%20window.md) 空间。

接收方 session 从零 context 开始——[model（模型）](./Model.md) 是 [stateless（无状态）](./Stateless.md) 的，旧 session 里没有任何东西对新 session 可见。下一个 session 需要什么，就必须显式携带什么；其余一切都没了。「无返回路径」是塑造携带方式的约束：新 session 没法问旧 session 那句话是什么意思，所以携带的材料必须自足。

| 载体 | 形态 | 性质 |
| ---- | ---- | ---- |
| Handoff artifact | [environment](./Environment.md) 里的文件 | 在任何东西依赖它之前你可阅读、可纠正；可跨多个 session 复用 |
| Compaction | context window 里的摘要 | 自动且便宜；难以检查；只服务一个后继者 |

糟糕 handoff 的可见失败是重翻旧案：新 session 重新打开旧 session 已经敲定的决定，因为携带物记下了决定了什么，没记为什么。评判一次 handoff 的标准：一个零 context 的 session 拿到它能做什么。

_用法：_

「规划 session 越来越重了——我该继续硬撑吗？」

「做一次 handoff。把决定写进一份文档，清空，在新 session 里读着它开始实现。」
