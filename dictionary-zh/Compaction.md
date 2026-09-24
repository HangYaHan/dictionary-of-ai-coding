---
description: 内存中完成的 handoff：上一个 session 的历史被总结，用来播种新 session。有损——拿细节换余量。
---

compaction（压缩）是在内存中完成的一次 [handoff](./Handoff.md)（交接）：上一个 [session](./Session.md)（会话）的历史被总结，总结用来播种一个新 session。设计上就是有损的：transcript（对话记录）是 [primary source](./Primary%20source.md)（一手来源），摘要是 [secondary source](./Secondary%20source.md)（二手来源）——拿细节换余量。由用户手动触发，或经 [autocompact](./Autocompact.md)（自动压缩）触发。

机制：[context window](./Context%20window.md)（上下文窗口）是有限的，长 session 会把它填满——每个 [tool result](./Tool%20result.md)（工具结果）、每次读文件、每个走错的 turn 都留在历史里。它变重之后，[harness](./Harness.md)（运行框架）请 [model](./Model.md)（模型）总结 session，把原始历史扔掉，用总结播种新 session。没进总结的东西就从 context（上下文）里消失了。有些 harness 缓解这一点：把旧 transcript 留在磁盘上，并在总结里留一个 [context pointer](./Context%20pointer.md)（上下文指针）指向它——二手来源链接回它的一手来源，总结丢掉的细节可以靠重读原件找回。

总结由 model 写成，所以可以提示它。「保住 schema 决定」会让生成的产物更有的放矢。时机也重要——在阶段边界 compact，计划敲定之后，而不是任务干到一半。

对比 [clearing](./Clearing.md)（清空）——它丢掉一切、从冷开始：compaction 试着把要点带过去；clearing 赌的是要点早已写在别处更好的地方。

_用法：_

"[context](./Context.md)（上下文）越来越重，而测试还没跑。"

"开始前先 compact——把必须活下来的内容写进总结提示，让新 session 保住 schema 决定、丢掉探索过程。"
