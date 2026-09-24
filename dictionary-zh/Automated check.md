---
description: 在环境中运行的确定性验证——测试、类型检查、lint、构建、pre-commit 钩子。通过/失败，无判断。
---

在 [environment](./Environment.md) 中运行的确定性验证——测试、类型检查、lint、构建、pre-commit 钩子。通过/失败，无判断。[agent](./Agent.md) 可据以自我纠正、无须牵扯他人的信号。一个 flaky 测试是坏掉的检查，不是非检查；automated checks 是 _设计上_ 确定的。

自我纠正以循环工作。agent 做一个改动，作为 [tool call](./Tool%20call.md) 跑检查，失败输出落进其 [context window](./Context%20window.md)——一个带文件和行号的类型错误，一个带期望值与实际值的断言失败。这足以让 agent 修复问题并再跑检查，转圈直到通过，环中无人。确定性使循环可信：相同代码总产生相同裁决，所以通过才有意义。Flaky 检查毒化这一点——agent 会"修复"本来没问题的代码，或重试越过真实失败。

这就是为什么好的检查是 codebase [AX](./AX.md) 的一大部分。在类型严格、测试套件快、有 linter 的仓库里，agent 多数错误在你看到之前就自纠了；在三者皆无的仓库里，它交付随手产出的东西。差别在 [AFK](./AFK.md) 运行中最要紧，那里检查是运行期间唯一的验证。但检查只捕捉它断言的东西——绿检查意味着断言的性质成立，不意味着代码正确。判断形状的空档是 [automated review](./Automated%20review.md) 和 [human review](./Human%20review.md) 的用途。

_避免：_"feedback loop" / "backpressure"——两者都把检查与 review 混在一起。_避免：_"test"——测试是 automated checks，但不是所有 automated checks 都是测试。

_用法：_

"AFK 运行里 agent 老是交付坏代码。"

"哪些 automated checks 接进了 [sandbox](./Sandbox.md)？"

"只有单元测试。"

"加上 typecheck 和 lint——PR 落地之前它会据这些自纠。"
