---
description: developer experience：代码库及其工具链让人类干好活有多容易——文档、反馈速度、错误。
aliases:
  - Developer experience
---

developer experience（开发者体验）——代码库及其工具链让人类干好活有多容易。好的 DX 是快速反馈、清晰的错误信息、答得上你真正问题的文档、一次就成的环境搭建。这个词远早于 AI 编码存在；它收入本词典主要是作为 [AX](./AX.md)（智能体体验）的对照。

DX 是人与代码库之间的交互——仅此而已。两类受众的主要差别是人是 [stateful](./Stateful.md)（有状态）的，agent（智能体）是 [stateless](./Stateless.md)（无状态）的。人把代码库学一次，此后每天都带着这份知识，所以差的 DX 活得下去：他们攒着推送绕过慢的 CI，在 Slack 问一次绕过缺失的文档，靠记住东西放哪绕过混乱的结构。变通不断累积，团队最终在一个跟他们作对的代码库里照样多产。

[Agents](./Agent.md)面对同一个代码库，却没有任何积累。跨 [sessions](./Session.md)（会话）无状态，agent 每次都从零重新学代码库——它受益于快的测试套件和清晰的错误信息，但它昨天弄明白的任何东西都没了，除非写进了 [environment](./Environment.md)（环境），而 agent 只经 [tool results](./Tool%20result.md)（工具结果）感知环境。这就是 AX 所命名的空隙：DX 中当开发者是 agent 时仍能存活的部分，加上人没有的顾虑，比如让 [context window](./Context%20window.md)（上下文窗口）保持空闲。

重叠意味着对 DX 的投入常顺带改善 AX——严格的类型、快的测试、可预测的结构对双方都有帮助。分岔意味着并不总是如此：一份漂亮的入门文档帮人帮一周，对 agent 则毫无用处，除非它能从 [AGENTS.md](./AGENTS.md.md) 抵达。

_用法：_

"我们 DX 不错——新人一周就能上手产出。"

"能产出是因为那一周有人带着他们。agent 没有那一周；AX 要单独查。"
