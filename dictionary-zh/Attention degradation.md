---
description: 随 session 增长，每个 token 的 attention budget 摊到更多竞争者；有意义关系上的信号变弱。
---

随 [session](./Session.md) 增长，每个 [token](./Token.md) 的 [attention budget](./Attention%20budget.md) 摊到更多竞争者。任何一条 [有意义关系](./Attention%20relationship.md) 上的信号缩小；无关 [context](./Context.md) 的噪声挤进来。同一个 [model](./Model.md)，同一组 [parameters](./Parameters.md)——只是同一盘饭要喂的嘴更多。smart zone / dumb [zone effect](./Smart%20zone.md) 的成因。

它表现为 model 会话中途变差：遵守了一小时的约束开始滑，它重问被告知过的事，写代码时忽略早先读过的文件。model 没有任何变化——唯一变量是它现在要在多大 context 上分配注意力。

它是渐进的，这正是从会话内部难以察觉的原因。没有报错，没有阈值；每个 [turn](./Turn.md) 只比上一个略差，等到滑手明显时，你已在 dumb zone 待了一阵。

恢复靠删 context，不靠加更多。重贴被忽略的指令是给同一拥挤窗口再添一个竞争者，只短暂有效。有效做法：[clear](./Clearing.md) 并只重载任务所需，或 [compact](./Compaction.md)，或 [hand off](./Handoff.md) 到全新会话。把指令遵从度下降当作 context 长度的信号，而非 model 的——换更大的 model 不解决，缩短 context 才解决。

_用法：_

"它深陷 dumb zone——编造 type 文件里没有的泛型。"

"Attention degradation。type 定义还在 context 里，但其信号被此后加入的一切埋了。Clear 后重载。"
