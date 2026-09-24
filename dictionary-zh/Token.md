---
description: 模型读写的原子单位。大致相当于词但不精确。Context window 大小、成本、延迟都以 token 计。
---

[model](./Model.md) 读写的原子单位。大致相当于词但不精确——常见词是一个 token，罕见词或长词拆成多个。[Context window](./Context%20window.md) 大小、成本和延迟都以 token 计量。

文本经 tokenizer（分词器）变成 token：一个在 [training](./Training.md) 之前学好的固定词表，含数万个片段，把任意输入切成词表条目序列。模型从不见到字符或单词——每段文本进入前都转成 token，[next-token prediction（下一 token 预测）](./Next-token%20prediction.md) 输出时一次产出一个 token。

经验法则：一个 token 约等于四分之三个英文单词，一千 token 约 750 词。代码更难预测：常见关键字和惯用写法编码紧凑，而生成的标识符、哈希、base64 块和压缩产物每个「词」拆成很多 token。规律是：在 tokenizer 训练素材中频繁出现的文本获得短而高效的编码；没出现过的被切成许多小块。像 `a3f9c2e1` 这样的哈希从未在任何地方出现过，所以拆成多个 token，而 `function` 就是一个。这就是为什么一个看起来不大、却充满罕见字符串的文件能占掉 context window 中惊人的份额。

Token 是衡量其他一切的单位。成本按 token 计——提供方分别对 [input tokens](./Input%20tokens.md) 和 [output tokens（输出 token）](./Output%20tokens.md)计费。速度是每秒 token 数，因为输出一次生成一个 token。而 context window 是固定 token 数，所以文件的 token 量决定了能装下多少。

_避免：_说「词」——token 边界和词边界并不重合，真正要紧的单位是 tokens-per-second 和 tokens-per-dollar。

_用法：_

「这个 prompt 会有多大？」

「跑一遍 tokenizer——schema 本身紧凑，但 JSON 键名怪，拆出来的 token 会比你想的多。」
