---
description: 为模型推理提供服务的一方。通常是远程的（Anthropic、OpenAI、Google），也可以是本地的（Ollama、llama.cpp）。
---

为 [model（模型）](./Model.md) 提供 [inference（推理）](./Inference.md) 的任何一方。通常是远程服务（Anthropic、OpenAI、Google），也可以是本地的——Ollama、LM Studio、跑在你自己机器上的 llama.cpp。[harness（运行框架）](./Harness.md) 不自己运行模型；它请求 provider 来跑。

provider 拥有整套机器：[parameters（参数）](./Parameters.md) 在它的硬件上，每次 [model provider request（模型提供商请求）](./Model%20provider%20request.md) 都是 harness 通过网络发送 [token（词元）](./Token.md) 并拿回预测。因此 provider 是一整类问题的来源，而这些问题常被错怪到模型或 harness 头上——速率限制、容量降级和故障都出在这里。当 [agent（智能体）](./Agent.md) 在 [session（会话）](./Session.md) 中途卡住，或每个 [turn（轮次）](./Turn.md) 都报错，先查 provider 的状态页再谈别的。

provider 还定下商业条款：[input tokens（输入词元）](./Input%20tokens.md) 与 [output tokens（输出词元）](./Output%20tokens.md) 的按 token 计价、[prefix cache（前缀缓存）](./Prefix%20cache.md) 折扣，以及哪些模型可用。注意 provider 和模型的开发商可以是不同公司——Bedrock、Vertex 和 OpenRouter 服务的是别人的模型。

本地 provider 用能力换控制：能塞进你自己硬件的模型远小于前沿模型，但没有东西离开机器，也没有按 token 的账单。

_用法：_

"能给气隙客户离线跑吗？"

"把 model provider 换成本地的——他们机器上装 Ollama 或 llama.cpp。harness 不在乎，它只是打另一个 endpoint。"
