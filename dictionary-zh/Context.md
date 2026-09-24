---
description: agent 此刻能访问的相关信息——agent 所知的、与任务切相关的内容。
---

context（上下文）是 [agent](./Agent.md)（智能体）此刻能访问的相关信息。一个抽象名词——不是 model（模型）看到的原始输入（那是 [context window](./Context%20window.md)（上下文窗口）），不是滚动的历史（那是 [session](./Session.md)（会话）），而是_agent 所知的、与任务切相关的东西_。「把某样东西载入 context」意为让它成为这个集合的一部分；「context engineering（上下文工程）」是策划这个集合的学问。

三个词分得干净：

| 术语 | 指什么 |
| -------------- | ------------------------------------------------------------------- |
| Context | agent 当前手头持有的、与当前任务相关的信息 |
| Context window | 每次请求中 model 实际看到的那串 [token](./Token.md)（词元） |
| Session | [harness](./Harness.md)（运行框架）存储的、进行中的对话 |

这个区分重要，因为 context 衡量的是质量，不是数量。context window 可以快满了而 context 依然糟糕——成千上万个 token 的过期工具输出，没有一样与手头任务相关。它也可以几乎是空的而 context 极好：那一个任务成败所依赖的 type 定义。

多数日常失败追溯到 context。当 agent 编造一个 API、与某个决定矛盾、或猜测 schema 时，第一个问题是它那么做时 context 里有什么——通常是相关事实从未被载入，或被压在 [attention degradation](./Attention%20degradation.md)（注意力衰减）之下。修法是策划：载入任务需要的，挡掉不需要的。

_用法：_

"它老编造 type 里没有的字段。"

"type 文件不在 context 里——它在读调用点然后猜。先把定义读进来。"
