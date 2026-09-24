---
description: 划定一次 session 工作范围的 handoff 产物。可独立存在或挂在 spec 下。可阻塞兄弟 ticket，也可被其阻塞。
---

划定一个 [session](./Session.md) 工作范围的 [handoff artifact（交接产物）](./Handoff%20artifact.md)。可独立存在，也可作为子项挂在 [spec](./Spec.md) 之下。Ticket 可阻塞兄弟 ticket，也可被其阻塞，所以工作顺序由它们的依赖图得出，而非线性计划。

决定性约束是尺寸：一个 session。Ticket 应在 session 漂出 [smart zone（智能区）](./Smart%20zone.md)之前完成——这个约束可检验。如果你的 ticket 上 session 经常在工作做完之前退化，ticket 太大；拆分。如果每个 session 把大部分 [context](./Context.md) 花在搭建上，只干五分钟活，ticket 太小；合并。

好的 ticket 写给毫无其他背景的读者：目标、验收标准，以及指向相关文件和决策的 [context pointer（上下文指针）](./Context%20pointer.md)——足够让 session 直接开工，不必重新推导上一个 session 已知的东西。

依赖图也是并行化的钥匙。独立的 ticket——图中的叶子——可各自在自己的 session 中同时运行。这是同时跑多个 agent 的有效方式。

_用法：_

「迁移 spec 该从哪开始？」

「看 ticket 图——schema 变更阻塞 backfill，backfill 阻塞 API 切换。挑个叶子，开个 session 跑。」
