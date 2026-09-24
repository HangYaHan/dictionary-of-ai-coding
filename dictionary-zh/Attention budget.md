---
description: 每个 token 都有有限的影响力，需分配给 context 其余部分。按 token 计，不随 context 增长。
---

每个 [token](./Token.md) 都有有限的影响力，要分配给 [context](./Context.md) 的其余部分。对 [一条关系](./Attention%20relationship.md) 影响重，留给其他的就少。预算按 token 计，不随 context 增长而增长，这就是长 [sessions](./Session.md) 被稀释的原因。

把它想成信号与噪声。你的指令是固定音量的信号；[context window](./Context%20window.md) 里每个其他 token 都是竞争的声响。指令从不变得更轻——它还在，一字一字都在——但 context 增长时，房间在它周围变得更吵，信噪比下降。在 10k token context 里最响的指令，到 150k 就是背景嗡鸣。这是 [attention degradation](./Attention%20degradation.md) 背后的机制：model 没忘记；信号淹没在噪声里。

症状表现为不服从——agent 早期同意了某个约束然后逐渐偏离，重新粘贴约束只短暂有效。原因不在指令；在窗口里与它竞争的一切。

你能控制的是什么进入 context。不服务任务的内容不是中性的——它是盖过一切有效内容的噪声。保持窗口小，在累积的 context 不再划算时 [clear](./Clearing.md)，并重述要紧的约束，而非指望早先的提及能一直顶用。

_用法：_

"为什么它一直忽略我贴在顶部的 schema？"

"我们早已进 [dumb zone](./Smart%20zone.md)——每个 token 的 attention budget 固定，context 却持续增长。schema 上的信号现在在和数千个更新的 token 竞争。"
