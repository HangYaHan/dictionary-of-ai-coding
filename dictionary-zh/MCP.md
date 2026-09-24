---
description: 把外部 tool server 接入 harness 的协议——agent 获得 harness 自带之外 tools 的方式。
---

**Model Context Protocol（模型上下文协议）。** 一个把外部工具服务器接入 [harness（运行框架）](./Harness.md) 的协议——[agent（智能体）](./Agent.md) 借此获得 harness 自带之外的 [tools（工具）](./Tool.md)。Agent 从不「调用 MCP」；它调用某个工具，而 harness 恰好是从一个 MCP server 那里得到这个工具的。MCP 也暴露资源（只读数据）和 prompts（可复用模板），但提供工具是主要用途。

这个协议解决的是集成问题。没有标准，每个 harness 都得有自己的 Linear 集成、自己的 Slack 集成、自己的数据库集成——各自单独编写和维护。有了 MCP，集成写一次、成为一个 server，任何兼容 MCP 的 harness 都能用它。Harness 连上 server，server 声明它提供哪些工具，这些工具就与内置工具并列，对 agent 可用。

代价付在 [context（上下文）](./Context.md) 上。Server 声明的每个工具都以一份定义到来——名字、描述、参数 schema——而 [model（模型）](./Model.md) 只能调用它知道的工具。朴素做法把每份定义都预先装进 [context window（上下文窗口）](./Context%20window.md)：装几个工具齐全的 server，一个 [session（会话）](./Session.md) 还没开打字就带着数千 [tokens](./Token.md) 的工具 schema 开始，[attention budget（注意力预算）](./Attention%20budget.md) 花在任务永远不会用的工具上。

许多 harness 现在用工具搜索缓解这一点：context 里不放完整定义，只放指向可用工具的 [context pointer（上下文指针）](./Context%20pointer.md)——agent 按名字或用途搜工具，需要时才载入它的定义。如果你的 harness 不这么做，前置成本照旧适用，值得做的只启用项目真正需要的 server。

_用法：_

「agent 需要从 Linear 读工单。」

「把 harness 配到 Linear MCP server——它把 Linear API 暴露成 agent 可调用的工具。省得你自己写工具包装。」
