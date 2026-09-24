---
description: 模型从训练中知道、存在 parameters 里的东西。训练时冻结。与 contextual knowledge 相对。
---

[model（模型）](./Model.md) 从 [training（训练）](./Training.md) 中"知道"、存在其 [parameters（参数）](./Parameters.md) 里的东西。训练时冻结——模型看不到也更新不了自己的 parameters。细节在挤压中丢失：数十亿事实塞进固定数量的 parameters，罕见的那些会模糊。常见话题流利的来源，罕见话题编造的来源。与 [contextual knowledge（上下文知识）](./Contextual%20knowledge.md) 相对。

parametric knowledge（参数化知识）不是以事实形式存储的。训练从不给模型一个查东西的数据库；它调整 parameters 直到模型把文本预测得好，而一个把某话题文本预测得好的模型，表现得像知道该话题。知识有多可靠，追踪某物在训练数据中出现的频率：有数百万例子的话题能准确复现，只有零星几个的，模型基于相似话题的样子来猜。对模型来说，复现和猜测是同一过程，所以它分不清自己在做哪个。编造的答案以同样的流利度到来。[hallucination（幻觉）](./Hallucination.md) 就是模型猜错了。

parametric knowledge 也会过期。parameters 在 [knowledge cutoff（知识 cutoff）](./Knowledge%20cutoff.md) 停止变化，所以该日期之后发布或改名的库在其中不存在，已改的 API 仍以旧形态被记住。

两类缺口——太罕见和太新——补法相同：知识加不进 parameters，只能作为 contextual knowledge 提供。

_用法：_

"它 React 写得无瑕，却在我们内部 SDK 上编方法。"

"React 在 parametric knowledge 里很密——数百万训练例子。你的 SDK 不是，所以模型填进看似合理的形状。把 SDK 文档装进 [context（上下文）](./Context.md)。"
