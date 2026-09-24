---
description: 通过海量文本喂给模型并调整参数以改进 next-token prediction 的过程，从而设定模型参数。
---

通过让 [model](./Model.md) 接触海量文本并调整 [parameters（参数）](./Parameters.md) 来改进 [next-token prediction](./Next-token%20prediction.md)，从而设定模型参数的过程。一次性的、昂贵的过程，由 [model provider（模型提供商）](./Model%20provider.md)完成。包含预训练（主体部分）和后训练（后续的指令遵循、安全等精修）；在本词表的层面，这个区分不重要。

机制是大规模重复：给模型看一段文本，让它预测下一个 [token](./Token.md)，把参数朝真实的下一个 token 微调，再在数万亿 token 上重复。没有任何东西以事实或规则的形式存储——模型「知道」的一切都是预测能力提升的副产品，作为[参数化知识](./Parametric%20knowledge.md)压缩在参数里。

两个后果在日常中要紧。Training 结束于某个时间点，所以模型有 [knowledge cutoff（知识截止）](./Knowledge%20cutoff.md)——它没见过你上个月升级的那个库版本。而且 training 不是你能做的事：当模型不了解你的代码库、你的约定或你的内部 API 时，解法从来不是「教模型」——而是把这些材料放进 [context](./Context.md)，那个你唯一能控制的输入。

_用法：_

「能不能让它知道我们的内部 API？」

「靠 training 不行——那是模型提供方历时数月的过程。把 API 文档加载进 context，那才是你真正有的杠杆。」
