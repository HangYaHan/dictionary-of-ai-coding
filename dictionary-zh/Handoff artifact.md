---
description: 作为 handoff 载体的文档——由一个 session 写下，供另一个 session 阅读。
---

用作 [handoff（交接）](./Handoff.md) 载体的文档——由一个 [session（会话）](./Session.md) 写入 [environment（环境）](./Environment.md)，供另一个 session 读取。[spec（规格说明）](./Spec.md)、[ticket（工单）](./Ticket.md) 和计划文档都是 handoff artifact（交接工件）。

要写它的理由：[model（模型）](./Model.md) 是 [stateless（无状态）](./Stateless.md) 的，session 里没有任何东西能在 [clearing（清空）](./Clearing.md) 后幸存。决定、约束、做到一半的计划——全随持有它们的 [context](./Context.md) 一起消失。environment 则持久。把重要状态写进文件，就是把它挪到下一个 session 能读回来的地方。

工件是 [secondary source（二手来源）](./Secondary%20source.md)——对 session 工作的记述，不是工作本身。这既是它小到能给一个全新 session 做简报的原因，也是它可能误导那个 session 的原因：它记下的是写下它的那个 session 相信的东西，遗漏或记错的部分对读者不可见。凡是要紧的主张，下一个 session 应当对照 [primary source（一手来源）](./Primary%20source.md)——代码、测试——核实，而不是直接继承。

好的工件是写给一个 context 为零的 session 读的。写具体文件路径，不写「我们讨论过的那个文件」。写清决定了什么、为什么决定，免得下一个 session 重翻旧案。写清做完了什么、还剩什么。告诉写它的 session 这份工件去哪儿也有帮助：「写一份交接文档，给一个对此工作一无所知的新 session」。

另一种载体是 [compaction（压缩）](./Compaction.md)，它在内存里做摘要。工件有两个优势：它落在磁盘上，你可以在任何东西依赖它之前阅读并纠正；它可以复用——同一份 spec 能给五个并行 session 做简报。

_用法：_

「这个怎么在规划 [agent](./Agent.md) 和实现代理之间拆？」

「让规划者写一份 handoff artifact——文件路径、决定、约束。实现者的 session 开局指向这份工件，把它当自己的简报来干活。」
