---
description: 结束当前 session 并开一个全新的。下一条消息从空 session 和空 context window 开始。
---

结束当前 [session](./Session.md)（会话），另起一个全新的。下一条消息从空 session 和空 [context window](./Context%20window.md)（上下文窗口）开始。通常由用户发起。

clearing（清空）是被污染的 context（上下文）的解药。session 累积一切：失败的尝试、走错的方向、过期的 [tool results](./Tool%20result.md)（工具结果）、被放弃的计划。[model](./Model.md)（模型）在每个 [turn](./Turn.md)（轮次）都把这些重读一遍，糟糕的历史拖累新工作。长 session 深处，[agent](./Agent.md)（智能体）变得含糊、不听话——你明确给过的指令被无视，质量下滑，催它做好也没用，因为它仍在其中跋涉的噪声还在 [context](./Context.md) 里。clearing 去掉这些噪声。

clearing 不会抹掉对话。多数 [harnesses](./Harness.md)（运行框架）把 session 历史存在你的电脑上，transcript（对话记录）仍可阅读或恢复。消失的是 agent 的工作状态：model 是 [stateless](./Stateless.md)（无状态）的，新 session 不知道旧 session 知道的任何事。如果 session 里存着下一个 session 需要的决定或进度，先让 agent 写一份 [handoff artifact](./Handoff%20artifact.md)（交接产物），再开新 session 指向它。

对比 [compaction](./Compaction.md)（压缩）——它把 session 总结进新 context，而不是从空开始。clearing 是更钝的工具：什么都不带过去，垃圾也不带。

_用法：_

"它卡在失败的测试上循环。"

"直接清空它——带着计划文档和测试文件开新 session。跟现有 context 较劲没意义。"
