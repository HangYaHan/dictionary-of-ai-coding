---
description: 模型内部的数字——常达数十亿——训练时调好。模型所知尽在其中。也称 weights。
---

[model（模型）](./Model.md) 内部的数字——常有数十亿个——在 [training（训练）](./Training.md) 中调好。模型"知道"的一切都在里面。训练设定它们；[inference（推理）](./Inference.md) 原样使用它们。也叫 _weights（权重）_。

机制上，parameters（参数）就是把输入变成输出的东西。[next-token prediction（下一词元预测）](./Next-token%20prediction.md) 是巨型计算：[context window（上下文窗口）](./Context%20window.md) 里的 [token（词元）](./Token.md) 进去，与 parameters 相乘，下一个 token 的预测出来。模型内部没有事实数据库，没有代码查找表——只有这些数字，排列成让计算倾向产出有用输出的样子。模型能从训练中背出的事实，比如标准库 API，是 [parametric knowledge（参数化知识）](./Parametric%20knowledge.md)：存在 parameters 里，不是从别处检索的。

值得内化的细节是：parameters 在训练后冻结。你在 [session（会话）](./Session.md) 里做什么都改不了它们——你的纠正、你给它看的代码库、它从中学到的错误都不行。每个 session 跑在同一组数字上。这就是模型 [stateless（无状态）](./Stateless.md) 的原因，也是它内置知识停在 [knowledge cutoff（知识截止）](./Knowledge%20cutoff.md) 的原因，还是任何项目特有内容必须经 [context（上下文）](./Context.md) 送达的原因。parameters 改变的唯一方式是更多训练——那实际上产出的是另一个模型。

_用法：_

"能在我们代码库上微调吗？"

"那会更新 parameters——之后就是另一个模型了。单个项目几乎总是把代码库当 context 加载比重训便宜。"
