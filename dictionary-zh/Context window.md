---
description: 模型每次 model provider request 看到的全部。有限、因模型而异，也是模型感知的唯一界面。
---

context window（上下文窗口）是 [model](./Model.md)（模型）在每次 [model provider request](./Model%20provider%20request.md)（模型提供商请求）中看到的全部内容。它有限、因模型而异，也是模型感知任何东西的_唯一_界面。

它是单一一串 [tokens](./Token.md)（词元）：[system prompt](./System%20prompt.md)（系统提示词）、到目前为止的对话、[harness](./Harness.md)（运行框架）反馈回来的每个 [tool result](./Tool%20result.md)（工具结果）。东西在那串里，model 就能用它；不在，model 就不知道它存在——不知道你的代码库、不知道你昨天编辑的文件、不知道你三个 session（会话）前给的指令。窗口之外的任何东西都要先被带进来（通常经一次 [tool call](./Tool%20call.md)（工具调用）），才能影响任何事。

有限意味着它会被填满。每个 turn（轮次）都追加更多——你的消息、model 的回复、tool result——长 [session](./Session.md)迟早撞上上限，迫使 [compaction](./Compaction.md)（压缩）或 [clearing](./Clearing.md)（清空）。这也意味着窗口里的一切在竞争：你载入的每个 token 都是本可留给其余内容的一个，你不需要的内容也仍占据 model 的 [attention](./Attention%20budget.md)（注意力预算）。实际的立场是把窗口当预算——载入任务需要的，留下其余。

_避免：_"memory"——context window 是工作状态，不跨 session 持久。[Memory](./Memory%20system.md)（记忆系统）是叠在其上的另一个概念。

_用法：_

"我能把整个 monorepo 粘进 prompt 吗？"

"context window 是 200k token——大概是仓库的五分之一。挑任务碰到的文件，其余的留在 tool call 后面。"
