---
description: 提供商侧的缓存，让连续请求跳过共享前缀的重复处理，这些 token 按更低费率计费。
---

[provider](./Model%20provider.md)（提供商）侧的缓存，让连续的[model provider requests](./Model%20provider%20request.md)（模型提供商请求）跳过共享前缀的重复处理。当一次请求的开头与最近一次的相同——同一个[system prompt](./System%20prompt.md)（系统提示词）、同一段历史直到某一点——provider 复用之前的工作成果，把这些[tokens](./Token.md)（词元）按[cache tokens](./Cache%20tokens.md)（缓存 token）计费，费率低得多。

缓存划算，因为[session](./Session.md)（会话）只追加增长。每次请求都把全部历史作为[input tokens](./Input%20tokens.md)（输入 token）重发（原因见该词条），而在正常 session 里历史只在末尾变化——每次请求是前一次加几条新消息。provider 把长长的共享开头处理一次、存下结果，再从缀前结束处接手。没有缓存，50 个[turn](./Turn.md)（轮次）的 session 要为第一轮付五十次全价处理费。

缓存也会过期。条目保持热的时长因模型提供商而异——通常按分钟算，不是小时。session 空闲超过窗口，下一次请求先按全价重建一次前缀，之后缓存才恢复。这主要是[harness](./Harness.md)（运行框架）构建者的关注点；作为用户，可见效果是长暂停后的请求比暂停前贵。

_用法：_

"为什么账单在 session 中途突然涨了？"

"harness 开始每轮把当前时间注入 system prompt。prefix cache（前缀缓存）在第一个变化的 token 处断裂，之后每个请求都按全价计费。"
