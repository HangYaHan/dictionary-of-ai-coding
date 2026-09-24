---
description: "model 自信地输出错误内容。两类：factuality（事实性）与 faithfulness（偏离已装入的 context）。"
---

自信地输出错误内容的 [model（模型）](./Model.md)。两类，成因和修法不同：

| 类别 | 错在哪 | 成因 | 修法 |
| ---- | ------ | ---- | ---- |
| _factuality（事实性）_ | 关于世界的事实编造或出错——不存在的函数、错误的 API 签名、虚假引用 | [parametric knowledge（参数化知识）](./Parametric%20knowledge.md) 的缺口，常在 [knowledge cutoff（知识截止）](./Knowledge%20cutoff.md) 之后 | 装入正确的 [contextual knowledge（上下文知识）](./Contextual%20knowledge.md) |
| _faithfulness（忠实性）_ | 输出偏离已装入的上下文知识、用户指令，或模型自己的先前推理 | [attention degradation（注意力衰减）](./Attention%20degradation.md)；在 [dumb zone（愚钝区）](./Smart%20zone.md) 中加重 | [clear（清空）](./Clearing.md) 或 [compact（压缩）](./Compaction.md) |

[Next-token prediction（下一 token 预测）](./Next-token%20prediction.md) 无论底层事实真假都产出流畅的文本——模型没有「我不知道某事」的内部信号，所以一个编造的方法以与正确方法相同的笃定口吻到来。幻觉出的代码按构造就显得可信：它正是这个 API _如果存在_ 会长的样子，而这恰恰让它滑过扫一眼式的审查，只在运行时才失败。

你得知道自己面对哪一类，因为修一类的方子会让另一类更糟。Factuality 意味着缺知识：修法是加 context——文档、类型定义、那个文件。Faithfulness 意味着知识在场，却在注意力竞争中输了：修法是减 context。把 faithfulness 误诊成 factuality，你会再粘更多文档，context 变大，漂移更重。agent 答错时，先查正确信息当时是否已在 context 里，再判断你遇的是哪种问题。

_避免：_ 把「hallucination」当作「错」的裸同义词——不点明类别，这个词没有诊断价值。

_用法：_

「它在 schema 上幻觉出一个 `parseAsync` 方法。」

「factuality 还是 faithfulness？」

「方法在我粘的文档里存在——它在第 [turn](./Turn.md) 四十之后就不读了。」

「那就是 faithfulness。压缩再重载，别加更多文档了。」
