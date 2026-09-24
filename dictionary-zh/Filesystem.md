---
description: agent 从中读取、写入并执行命令的文件与目录树——编码 agent 的默认环境。
---

一个 [agent（智能体）](./Agent.md) 从中读取、写入并在其中执行命令的文件与目录树——编码 agent 默认的 [environment（环境）](./Environment.md)。[AGENTS.md](./AGENTS.md.md)、[skills](./Skill.md)、源代码、构建脚本和 [tool（工具）](./Tool.md) 配置都住在 filesystem（文件系统）里。当一个 [harness](./Harness.md)「在你的项目里启动」，它做的就是把 agent 指向一个 filesystem。

agent 只通过 [tool call（工具调用）](./Tool%20call.md) 接触 filesystem——读一个文件、写一个文件、跑一条 shell 命令。磁盘上的东西在 tool call 把它载入之前都不在 [context window（上下文窗口）](./Context%20window.md) 里，这正是 agent 能在远大于窗口的仓库里工作的前提：filesystem 装下一切，context 只装当前任务读过的那部分。有些 harness 默认把当前目录的文件名载入 context window——不是内容，只是目录树——它们充当 [context pointer（上下文指针）](./Context%20pointer.md)：agent 看见有什么存在，再读它需要的文件。

filesystem 也与你共享。agent 编辑的文件就是你在编辑器里打开、在 git 里做 diff 的那些——它是你审查 agent 所做之事的公共工作区。agent 写完文件，你刷新编辑器就能看到；反过来，你改了文件，只要它下次用 tool call 去读，读到的就是你改过的版本。

_用法：_

「它为什么没读到我的 AGENTS.md？」

「它跑在另一个 filesystem 上——[sandbox](./Sandbox.md) 挂载了父目录，不是项目根。把 harness 重新指过去。」
