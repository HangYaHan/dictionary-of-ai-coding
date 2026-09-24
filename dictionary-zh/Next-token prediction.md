---
description: 模型实际在做的事。从 context 采样一个下一 token，追加，再跑。唯一的运行方式。
---

[model（模型）](./Model.md) 实际在做的事。给定 [context（上下文）](./Context.md)，它采样一个下一个 [token（词元）](./Token.md)，追加，再跑。每份输出——一句话、一个 [tool call（工具调用）](./Tool%20call.md)、一个千行文件——都是一次一个 token 建起来的。模型没有别的运行方式。

每步机制相同：[context window（上下文窗口）](./Context%20window.md) 里的 token 过一遍 [parameters（参数）](./Parameters.md)，对词表里每个 token 产生一个概率——这个很可能是下一个，那个低一些。从这些概率里采样一个 token，追加，循环带着略长的 context 再来一次。正因为有这个采样步骤，同一 prompt 不同次跑出不同输出：[non-determinism（非确定性）](./Non-determinism.md) 内建于机制本身，不是叠在上面的 bug。

抓住这个机制，就能解释 otherwise 显得奇怪的行为。模型发出 token 前从不检查它是否_真_，只检查它是否_可能_——这是 [hallucination（幻觉）](./Hallucination.md) 的根。它逐 token 愿赌服输，所以一句听来自信的开头能把余下答案带偏。而且 [output tokens（输出词元）](./Output%20tokens.md) 严格一次一个地产生，生成速度给任何 [agent（智能体）](./Agent.md) 的工作速度定了下限。

_用法：_

"agent 怎么'决定'调用工具？"

"它不决定——一路都是 next-token prediction。tool call 只是 [harness（运行框架）](./Harness.md) 从输出流里解析出来的结构化字符串。"
