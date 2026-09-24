---
description: 对一手来源的转述，隔了一层——摘要、文档、压缩总结。载入便宜，构造上必有损。
---

对 [primary source（一手来源）](./Primary%20source.md) 的转述，隔了一层——描述代码的文档、描述记录的摘要、描述搜索结果的报告。载入 [context window（上下文窗口）](./Context%20window.md) 比它所描述的来源便宜，且构造上有损：写它的人决定了什么重要，而被他丢掉的，对只有摘要的读者不可见。

很大一部分 [context（上下文）](./Context.md) 工程就是在制造二手来源。[Compaction（压缩）](./Compaction.md) 把 [session（会话）](./Session.md) 历史变成摘要，为下一个 session 打底。[Subagent（子智能体）](./Subagent.md) 在嘈杂搜索中烧掉自己的 context，返回一份短报告。[Handoff artifact（交接产物）](./Handoff%20artifact.md) 把一个 session 的决定浓缩成下一个 session 读的文档。[Memory system（记忆系统）](./Memory%20system.md) 把 session 所学蒸馏成笔记。每一笔交易相同：保真度换余量。

Secondary source（二手来源）有两种失败方式。一是有损——丢了 schema 决策的压缩摘要、没提边界情况的报告。二是漂移——一手来源变了而转述没跟上，于是文档以本季度的笃定描述上季度的架构。当 [agent（智能体）](./Agent.md) 基于任一种已失败的二手来源行动，它就在错误信息上自信地工作；解法是把它送回一手来源。

两种失败都不说明二手来源是错误选择。Context window 有限，一手来源昂贵；没有摘要、报告和交接文档，任何大东西都装不下。功力在于知道哪些细节能在损失中幸存——以及当某处不能时，向一手来源核对。做得好的二手来源带着一个 [context pointer（上下文指针）](./Context%20pointer.md) 指回原件——点名它所据记录的摘要、点名它所描述文件的文档——这样转述不够用时，读者能顺指针走，而不是在损失上工作。

_用法：_

"交接文档说 auth 做完了，可新 session 一直发现 token 刷新是坏的。"

"文档是二手来源——上一个 session 写下的是它相信的，不是真实的。让新 session 跑 auth 测试，信一手来源。"
