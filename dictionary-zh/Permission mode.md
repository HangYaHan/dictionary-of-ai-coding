---
description: agent mode 中权限门控的切片——哪些 tool call 触发 permission request，哪些自动执行。
---

[agent mode（智能体模式）](./Agent%20mode.md) 中权限门控的切片——哪些 [tool call（工具调用）](./Tool%20call.md) 触发 [permission request（权限请求）](./Permission%20request.md)，哪些自动运行。[harness（运行框架）](./Harness.md) 开始在其上捆绑行为指令之前，模式系统的原始用途。

harness 出货这样一组模式阶梯：

| 模式               | 读取 | 写入与 shell          | 典型用途                              |
| ------------------ | ---- | ---------------------- | ------------------------------------- |
| 只读 / plan        | 自动 | 阻止                   | 调研、规划、评审                      |
| 默认               | 自动 | 询问                   | 日常有监督工作                        |
| 自动编辑           | 自动 | 编辑自动，shell 询问   | 受信仓库、机械改动                   |
| "Yolo" / 全自动    | 自动 | 自动                   | [Sandbox（沙箱）](./Sandbox.md)、[AFK](./AFK.md) 运行 |

选哪一级是安全与打断之间的取舍，两种失败模式都会被感觉到。太紧，你就成了瓶颈：[agent（智能体）](./Agent.md) 每几秒为无害读取停下，你在自动驾驶式点批准，批准也不再有意义——橡皮图章是最坏的组合，全打断、零保护。太松，agent 会编辑文件、跑命令，而那些你本想先看一眼。

松的那端在 sandbox 里最站得住脚，那里坏 [tool](./Tool.md) call 的爆炸半径被圈住。在 sandbox 之外，多数人折中为：读取自动批准，任何不可逆操作保留 [human-in-the-loop（人在回路）](./Human-in-the-loop.md)。

_用法：_

"它每个 grep 都停——AFK 运行彻底废了。"

"对只读工具放宽 permission mode，写入和 shell 继续问。调研 [session（会话）](./Session.md) 上多数 permission request 是噪音。"
