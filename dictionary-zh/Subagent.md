---
description: 由另一个 agent 通过 tool call 派生的 agent。在自己的 session 中运行，返回单一 tool result，不能再生子 agent。
---

由另一个 [agent](./Agent.md) 通过 [tool call](./Tool%20call.md) 派生的 agent。在自己的 [session](./Session.md) 中运行，拥有独立的 [context window（上下文窗口）](./Context%20window.md)，结束后向父级返回单个 [tool result](./Tool%20result.md)。与 [handoff（交接）](./Handoff.md) 不同——父级明确期待返回结果；handoff 没有返回路径。**不能再生子 agent**——树只有一层深。Subagent 存在的目的是隔离 [context](./Context.md)，不是构建层级结构。

其意义在于把嘈杂工作挡在父级 context 之外。一次宽泛搜索或长篇文件阅读会产生大量 tool result，其中多数只在找到答案之前有用。放在父级里跑，这些内容会留在父级 context 中占满整个 session；放在 subagent 里跑，噪音填入一个用完即弃的窗口——只有最终报告进入父级 context。报告是[二手来源](./Secondary%20source.md)：父级看到的是 subagent 对发现内容的转述，不是原始结果，所以报告遗漏的内容对父级不可见。

Subagent 还可并发运行——父级可同时扇出多个，处理相互独立的工作。

_用法：_

「grep 结果快把我的 context 撑爆了。」

「派个 subagent 去搜——让它烧自己的 context window 承担噪音，只回报你真正需要的两个文件路径。」
