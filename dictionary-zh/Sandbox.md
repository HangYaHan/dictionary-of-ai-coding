---
description: agent 运行于内的隔离环境——容器、虚拟机或受限 shell。限制 agent 动作的爆炸半径。
aliases:
  - Sandboxing
  - Sandbox / Sandboxing
---

Agent（智能体）运行于内的隔离 [environment（环境）](./Environment.md)——容器、VM（虚拟机）、临时 [filesystem（文件系统）](./Filesystem.md)，或受限权限的 shell。限制 agent 动作的爆炸半径：即使 agent 跑了破坏性命令或抓取了恶意内容，损害也被圈住。这是让 [AFK](./AFK.md) 可行的安全底座。

Sandbox（沙箱）与 [permission mode（权限模式）](./Permission%20mode.md) 从两端解决同一问题。权限在动作运行前发问；沙箱限制动作运行后能触及什么。权限需要你在 [in the loop（人在回路）](./Human-in-the-loop.md) 中——每次提示都是一次打断——不断提问的 session（会话）几乎谈不上自主。沙箱花基础设施而非注意力：隔离越强，需要问的问题越少。

隔离分等级：

| 等级 | 是什么 | 圈住什么 |
| --- | --- | --- |
| 受限 shell | 围绕每条命令的 OS 级禁闭 | 项目外写入、网络访问 |
| 容器 | 全新文件系统、不挂载凭证、用后即弃 | agent 对自己机器做的一切 |
| VM / 云 | 完全独立的机器，常由 [harness（运行框架）](./Harness.md) 提供 | 一切，包括内核级逃逸 |

没有什么沙箱圈得住合法离开它的动作。持有你 git 凭证的 agent 能推送；有网络访问的 agent 能调生产 API。先决定什么越过边界，再决定边界做多厚。

_用法：_

"我想让它整夜跑 [bypass-permissions（绕过权限）](./Agent%20mode.md)，但我还没准备好。"

"放进沙箱——全新容器、不挂载凭证、无出网。最坏情况它毁掉自己的文件系统，你把容器丢掉。"
