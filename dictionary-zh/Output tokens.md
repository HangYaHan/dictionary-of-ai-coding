---
description: 模型生成回来的 token。计费高于 input tokens，因为产生它们的算力开销更大。
---

[model（模型）](./Model.md) 生成回来的 [token（词元）](./Token.md)。计费高于 [input tokens（输入词元）](./Input%20tokens.md)——通常约五倍费率——因为产生它们要花更多算力。

模型写的一切都算：你读到的散文、它吐出的代码、[tool call（工具调用）](./Tool%20call.md)，以及模型回答前做的任何 extended thinking（扩展思考）。最后一项常让人意外——reasoning token（推理词元）按输出计费，即便 [harness（运行框架）](./Harness.md) 常常根本不展示给你，而调高 [effort（努力度）](./Effort.md) 会花掉更多它们。

output tokens（输出词元）也定下 [session（会话）](./Session.md) 的节奏。模型读输入快，生成输出却一次一个 token，所以当一个 [turn（轮次）](./Turn.md) 感觉慢，几乎总是输出在写，不是输入在读。等很久通常意味着一个长答案要来了。

_用法：_

"重构会话把额度烧穿了，输入明明不大。"

"agent 在整文件重写而不是打补丁。output tokens 费率约为 input 的五倍——让它吐编辑，账单就降。"
