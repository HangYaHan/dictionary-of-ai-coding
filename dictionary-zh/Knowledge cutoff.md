---
description: 晚于该日期的 model 没有 parametric knowledge。cutoff 之后的库和 API，不载入文档就是编造陷阱。
---

晚于该日期，[model（模型）](./Model.md) 就没有 [parametric knowledge（参数化知识）](./Parametric%20knowledge.md)。cutoff 之后的库、API 和事件，除非其文档作为 [contextual knowledge（上下文知识）](./Contextual%20knowledge.md) 载入，否则都是编造陷阱。每次 model 发布都带着自己的 cutoff；同一家的不同型号 cutoff 也不同，换型号时这一点容易被忘掉。

Cutoff 之所以存在，源于 model 的造法：[training（训练）](./Training.md) 把一份文本快照烤进 model 的 [parameters（参数）](./Parameters.md)，此后 parameters 冻结。Model 不知道自己的知识有边界——问到 cutoff 之后的事，它不拒绝，而是从最近的已知处外推。这就是陷阱安静的原因：针对旧版本库写的代码看起来可信，常常还能编译，在改动过的部分才失败——改名的函数、变掉的默认参数、挪了位置的符号，模型仍按训练时见过的旧形态写出来。

修法始终一样：把当前信息弄进 [context（上下文）](./Context.md)。载入 changelog，指向已安装版本的类型定义，或让 agent 从网上读当前版本的文档，而不是靠记忆作答。context 里的任何东西都胜过 parameters 里的「没有」。

_用法：_

「它老写 v3 SDK 的语法——我们在用 v5。」

「v5 发布在 knowledge cutoff 之后。把 v5 的 changelog 载成 contextual knowledge，否则它会一直按旧的 parametric 版本编。」
