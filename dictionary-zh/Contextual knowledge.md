---
description: agent 此刻可直接从 context 读到的事实。与 parametric knowledge 相对。
---

contextual knowledge（上下文知识）是 [agent](./Agent.md)（智能体）此刻可直接从 [context](./Context.md)（上下文）读到的事实——用户的任务、agent 已读入的文件、[tool results](./Tool%20result.md)（工具结果）、[session](./Session.md)（会话）开始时加载的 [AGENTS.md](./AGENTS.md.md) 内容。与 [parametric knowledge](./Parametric%20knowledge.md)（参数化知识）相对：parametric 从 parameters（参数）里_回忆_；contextual 从 [window](./Context%20window.md)（窗口）里_读_。[Hallucinations](./Hallucination.md)（幻觉）在 agent 从 contextual knowledge 工作时少得多——答案就在它面前，不是从模糊的记忆里捞出来的。

两类知识里，只有 contextual knowledge 受你控制。parameters 是冻结的，所以给 [model](./Model.md)（模型）补上它缺的知识——一个内部 SDK、一个 [knowledge cutoff](./Knowledge%20cutoff.md)（知识 cutoff）之后发布的库、一个昨天做出的决定——唯一的办法就是把它放进 context。大量实际的 [AI](./AI.md) 编码工作归结于此：在 model 需要的那一刻，把对的事实摆在它面前。

contextual 与 parametric 知识冲突时，contextual 通常赢。贴上当前 API 文档，model 就照它做，而不是凭对旧 API 的过时记忆——尽管旧版本仍会渗出来，长 session 深处尤其如此。文档已载入而 agent 还是回到过时写法，那是 parametric knowledge 漏过了 contextual；重述那条纠正，或把它挪得离工作更近，会有帮助。

与 parametric knowledge 不同，contextual knowledge 用起来有成本。载入窗口的一切都花 [tokens](./Token.md)（词元），并争夺 model 的 [attention budget](./Attention%20budget.md)（注意力预算），所以载入更多并不自动更好——目标是让相关事实在窗口里，不是所有事实。

_只有在与 parametric knowledge 对比时才用这个词_；其余时候直接说 **context**。

_避免：_"working memory"——contextual knowledge 是窗口_此刻_里的东西；[memory system](./Memory%20system.md)（记忆系统）是把跨 session 内容弄进窗口的东西。尺度不同，别混。

_用法：_

"为什么我贴文档它就 API 全对，不贴就编？"

"文档在，就是 contextual knowledge——照着页面读。不在，就是 parametric，罕见的 endpoint 就糊了。"
