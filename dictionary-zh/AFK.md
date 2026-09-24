---
description: 一种工作模式：用户发起会话后离开，让 agent 无人值守地运行（away from keyboard）。
aliases:
  - away from keyboard
  - AFK (away from keyboard)
---

Away from keyboard（离开键盘）。一种工作模式：用户发起一个 [session](./Session.md) 后离开，让 [agent](./Agent.md) 无人值守地运行。这是 [AI](./AI.md) 编程的吞吐倍增器——你睡觉、吃饭或做别的事时，多个 AFK 会话可以并行跑。通常需要较宽松的 [permission mode](./Permission%20mode.md) 配合 [sandboxing](./Sandbox.md) 才安全。

你不在场时，agent 处理歧义的方式不同。你在看着时，有歧义的决定会浮出来变成一个问题，由你回答；一旦你走开，agent 会选一个默认值继续走，之后每个决定都建立在那个猜测上。典型的失败是：你回来后发现几小时已完成、充满自信的工作，全建立在最初十分钟的一个错误判断上。工作并不粗糙——它自洽，只是自洽在错的东西上。

运行期间你无法给输入，所以改在之前和之后给。之前：先把歧义解决掉——一轮 [grilling](./Grilling.md) 会话，一份书面 [spec](./Spec.md)——这样 agent 独自填补的空隙更少。期间：[automated checks](./Automated%20check.md) 和 [automated review](./Automated%20review.md) 顶替你没付出的注意力，对能机械捕捉的问题快速失败。之后：运行结束时产出可审查的东西——一个 PR，而不是已合并的改动。AFK 不取消 [human review](./Human%20review.md)；它把全部审查推迟到最后，所以最后送达的东西必须值得审。这也解释了为什么 [AX](./AX.md) 在 AFK 运行中最重要——没人看着时，环境是 agent 唯一能依靠的支持。

_避免：_"background agent"——以机器为中心（"在后台运行"），而非人的模式（"用户已走开"）。AFK 命名的是要紧的事实：用户没在看。

_用法：_

"我在 AFK 跑这个——三个 sandbox 里的 agent 做重构，早上审 PR。"

"[Bypass permissions](./Agent%20mode.md)？"

"嗯，只读 [filesystem](./Filesystem.md)，无网络。"
