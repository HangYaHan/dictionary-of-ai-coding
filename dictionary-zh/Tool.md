---
description: harness 暴露给 agent 调用的函数——Read、Write、Bash、Search。agent 感知并作用于环境的方式。
---

[harness](./Harness.md) 暴露给 [agent](./Agent.md) 调用的函数——Read、Write、Bash、Search。Tool（工具）是 agent 感知并作用于 [environment（环境）](./Environment.md)的方式：除了通过 [tool result](./Tool%20result.md) 它看不见环境，除了通过 [tool call](./Tool%20call.md) 它改不了环境。每次 tool call 额外花费一次 [model provider request](./Model%20provider%20request.md)，因为结果必须先回到模型，模型才能决定下一步。

多数编码 agent 自带的工具：

| 工具 | 作用 |
| ---- | ---- |
| Read | 把文件内容作为 tool result 返回 |
| Write | 在 [filesystem（文件系统）](./Filesystem.md)中创建或编辑文件 |
| Bash | 运行 shell 命令并返回其输出 |
| Search | 在代码库中查找匹配模式的文件或文本 |

一个工具由三样东西定义：名字、作用描述、参数 schema。Harness 随每次请求把这些定义发给 [model](./Model.md)，模型选择工具的方式和产生其他一切相同——写 [token](./Token.md)，此处是带参数的结构化调用。模型从不亲自执行任何东西；harness 读取调用、运行函数、送回结果。

工具清单决定了 agent 能做什么。能力再强的模型配上狭窄的工具集也是狭窄的 agent：它会把一切都路由到手头已有的工具上，这就是 agent 如此重度依赖 Bash 的原因——shell 是一个能触及系统大部分地方的工具。要干净地赋予 agent 某项能力，就给它加一个工具；[MCP](./MCP.md) 是从 harness 外部接入工具的标准。

Tool 定义在每次请求中都占用 [context](./Context.md)，所以大型工具集在任何工具被调用之前就有固定开销——而且许多描述相似的工具会让模型更难选对。

_用法：_

「agent 能直接查 staging 吗？」

「给 harness 加个 `psql` 工具，staging 上限只读。没有这个工具，agent 对 filesystem 之外一无所知。」
