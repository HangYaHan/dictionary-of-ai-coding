---
description: 向前携带信息。session 跨 turn 有状态；agent 可经记忆系统跨 session 有状态。
---

向前携带信息。[Session（会话）](./Session.md) 跨 [turn（轮次）](./Turn.md) 有状态——[context（上下文）](./Context.md) 随 session 运行而累积，这就是长 session 漂入 [dumb zone（愚钝区）](./Smart%20zone.md) 的原因。[Agent（智能体）](./Agent.md) 可以通过加入 [memory system（记忆系统）](./Memory%20system.md) 跨 **session** 变为有状态：把信息持久化进 [environment（环境）](./Environment.md)，在未来 session 开头重新载入。[Model（模型）](./Model.md) 永远不是有状态的；任何看似连续都是 [harness（运行框架）](./Harness.md) 在回灌 context。与 [stateless（无状态）](./Stateless.md) 相对。

各层状态所在处：

| 层 | 有状态？ | 如何 |
| --- | --- | --- |
| Model | 从不 | [Parameters（参数）](./Parameters.md) 冻结；它只看到每个请求里的东西 |
| Session | 跨 turn | harness 把每条消息和 [tool result（工具结果）](./Tool%20result.md) 追加进 context |
| Harness | 跨 session | 记忆文件、[AGENTS.md](./AGENTS.md.md)、[handoff artifacts（交接产物）](./Handoff%20artifact.md)——写下来，稍后重载 |
| Environment | 总是 | 文件是否持久与有无 session 在跑无关 |

每层的有状态性，靠重读更低一层存的东西建成：session 感觉连续，因为 harness 把消息历史重发给无状态的 model；agent 跨 session 记得，因为 harness 从 environment 重载文件。状态从不存在 model 本身里。

状态不总是可取。向前携带的一切影响之后，所以 session 早期做出的错误假设也会被向前携带。[Clearing（清空）](./Clearing.md) 是刻意丢弃 session 状态、从写下的东西重新开始的行为。

_用法：_

"它记得我昨天的偏好——是 model 学会了吗？"

"不是，agent 有状态是因为 harness 把偏好写进了记忆文件、在 session 开头重载。model 本身对昨天一无所知。"
