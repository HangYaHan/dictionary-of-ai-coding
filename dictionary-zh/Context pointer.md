---
description: 一处指向另一文档的提及，让 agent 只在任务需要时才把它拉进 context。
---

一处指向另一文档的提及，让 [agent](./Agent.md)（智能体）只在任务需要时才把它拉进 [context window](./Context%20window.md)（上下文窗口）。[progressive disclosure](./Progressive%20disclosure.md)（渐进式披露）由这样的单元构成。

用 pointer（上下文指针）而不是把内容内联，理由是成本。pointer 在 context window 里只占一行。它背后的文档可能有数千 [tokens](./Token.md)（词元），但 agent 真正跟随 pointer 之前，这些 token 不花钱。把一份 2,000 token 的运行手册内联进 [AGENTS.md](./AGENTS.md.md)，每个 [session](./Session.md)（会话）都要为它付费；换成「部署流程：见 `internal/deploy.md`」，就只有会部署的 session 才加载它。任务对上时，agent 用一次 [tool call](./Tool%20call.md)（工具调用）跟随 pointer。

pointer 要能工作需要两部分：稳定的路径，以及足够的描述，让 agent 知道何时值得跟随它。光秃秃的路径，agent 没有理由跟随；「见 `internal/deploy.md`」却不提示里面有什么，会被正需要它的 session 跳过。写这一行要贴合任务出现的方式：「发版、部署或回滚——先读 `internal/deploy.md`」。

留意的话，pointer 到处都是：AGENTS.md 里的行、[skill](./Skill.md)（技能）的描述——harness（运行框架）加载描述，skill 的正文在后面等着——目录列表里的文件名、文档之间的链接。

pointer 还能把 [secondary source](./Secondary%20source.md)（二手来源）拴回它所源自的 [primary source](./Primary%20source.md)（一手来源）——点名原始 transcript（对话记录）的 compaction（压缩）总结、点名所描述源文件的文档。这让二手来源的有损变得可恢复：总结被证明不够用时，agent 跟随 pointer 去读原件，而不是在总结留下的东西上工作。

_避免：_"reference"——太干，传达不出跟随它会拉进更多 context（上下文）的意思。"Portal"——太花。

_用法：_

"AGENTS.md 越来越大。"

"大部分该是 context pointer（上下文指针），不是内容。常开规则留在内联；把部署手册和风格指南做成 skill，后面留个 context pointer。"
