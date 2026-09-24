---
description: harness 在执行未经预批准的 tool call 前展示给用户的内容。让人进入 loop 的机制。
---

[harness（运行框架）](./Harness.md) 在执行未经预批准的 [tool call（工具调用）](./Tool%20call.md) 前展示给用户的东西。[model（模型）](./Model.md) 产出 tool call；harness 不立即运行，而是暂停并询问。批准则运行；拒绝则 harness 把拒绝作为 [tool result（工具结果）](./Tool%20result.md) 报回模型。harness 让人在风险或敏感操作的 [loop（回路）](./Human-in-the-loop.md) 中的机制。

permission request（权限请求）的生命周期：

| 步骤 | 谁      | 发生什么                                                                                |
| ---- | ------- | --------------------------------------------------------------------------------------- |
| 1    | 模型    | 产出一个 tool call                                                                      |
| 2    | harness | 对照 [permission mode（权限模式）](./Permission%20mode.md) 和已保存的批准检查它         |
| 3    | harness | 已预批准：立即执行。否则：暂停并展示请求                                                 |
| 4    | 用户    | 批准一次、批准本 [session（会话）](./Session.md) 剩余部分，或拒绝                        |
| 5    | harness | 执行该调用，或把拒绝作为 tool result 发回                                                |

拒绝请求会给 agent 导向。模型像读任何 tool result 一样读拒绝并作出反应——换条路子，或问你更想要什么。多数 harness 允许你在拒绝上附一条消息，把请求变成一个导向点："别那样，用迁移脚本"——正好落在模型决定下一步做什么的时刻。

代价是每个请求都是对你的一次同步等待。[agent（智能体）](./Agent.md) 阻塞到你回答为止，你在看着时没问题，不在时就是问题——频繁触发请求的 agent 没法留着 [AFK](./AFK.md) 干活。permission mode 就是那个旋钮：哪些调用自由跑、哪些先问，理想情况下配一个 [sandbox（沙箱）](./Sandbox.md)，让扩大自由集变得安全。

_用法：_

"它卡在 permission request 上十分钟了——我在开会。"

"这就是 human-in-the-loop 的代价。预批准安全的 [tool（工具）](./Tool.md)，让请求只在真正有风险的调用上触发。"
