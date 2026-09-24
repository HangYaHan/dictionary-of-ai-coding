---
description: 模型输出中指明 tool 及其参数的内容——只是结构化文本。须由 harness 读取并执行。
---

[model](./Model.md) 输出中指明 [tool](./Tool.md) 及其参数的部分——只是结构化文本。它自己什么也不做；[harness](./Harness.md) 必须读取并执行。由模型在一次 [model provider request](./Model%20provider%20request.md) 中产生。

Tool call（工具调用）的生命周期：

| 步骤 | 谁 | 发生什么 |
| ---- | -- | -------- |
| 1 | 模型 | 从 [system prompt](./System%20prompt.md) 中的描述得知有哪些工具 |
| 2 | 模型 | 产出一个调用——工具名加参数，通常是 JSON——然后停下 |
| 3 | Harness | 解析调用，对照 [permission mode（权限模式）](./Permission%20mode.md)检查 |
| 4 | Harness | 允许则执行 |
| 5 | Harness | 在下一次请求中把结果作为 [tool result](./Tool%20result.md) 送回 |

一个 [turn](./Turn.md) 的 [agent](./Agent.md) 工作通常是许多次这样的往返串联而成。

因为调用和其他一切一样由 [next-token prediction](./Next-token%20prediction.md) 生成，它可能以任何模型输出会出错的方式出错：不存在的路径、命令没有的旗标、看似合理而非正确的参数。Harness 执行写下的内容，不是想表达的内容——打错的路径不会优雅报错，而是编辑错误的文件。

_用法：_

「它说跑了测试，但文件时间戳没变。」

「看 transcript——它真的发出了 tool call，还是只是描述了跑测试？调用由模型产出，但 harness 没执行就什么都没发生。」
