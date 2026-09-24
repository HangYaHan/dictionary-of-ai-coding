---
description: 两个 token 之间的配对——有意义的对比不相关的对互相影响更强。N 个 token 的 context 有约 N² 个这种关系。
---

预测每个 [token](./Token.md) 时，[model](./Model.md) 会把 [context](./Context.md) 里每个其他 token 计入——有的权重很大，有的几乎没有。两个 token 之间的配对就是一条 **attention relationship**，有意义的对（"她"和"Sarah"，或一个 `getUser()` 调用与它的 `function getUser` 定义）比不相关的对互相影响更强。N 个 token 的 context 有约 N² 量级的关系。

配对是 model 表面理解所在之处。它能解析代词，是因为 "her" 和 "Sarah" 之间的 attention relationship 强。它用正确参数调用函数，是因为调用点与它早先读过的定义之间的关系在起作用。这些都不是查出来的——每次 [model provider request](./Model%20provider%20request.md) 都对每一对重新算出。

N² 这个数值得细想，因为它比直觉暗示的长得快：

| Context 大小   | 配对数（~N²）  |
| -------------- | -------------- |
| 1,000 tokens   | 约100万        |
| 10,000 tokens  | 约1亿          |
| 100,000 tokens | 约100亿        |

每个配对还不止算一次。model 有多个 attention head——前沿 model 的确切数字未公布，但五十到一百是合理猜测——每个 head 计算自己版本的每条关系。所以表中每个配对在每个 head 上都复制一份。配对数量很大。

任何给定任务里只有少数关系要紧。你的指令与它管辖的代码之间的配对是少数算数的之一；池子里几乎所有其他都是噪声。两者增长率不同：要紧的关系大致恒定，而总池子随 context 大小平方增长。1,000 token 时，你在意的配对是百万分之一；100,000 token 时，是百亿分之一。这是 [attention budget](./Attention%20budget.md) 底下的算术，而 [attention degradation](./Attention%20degradation.md) 是要紧关系分到的份额太薄时的感受。

_用法：_

"它总把 diff 两侧的两个 `user` 符号搞混——听像我们进了 [dumb zone](./Smart%20zone.md)。"

"是，每个调用点与其声明之间的 attention relationship 在和另一个打架——token 形状相同，绑定不同。重命名一个，配对就清晰了。"
