---
description: 调节 model 回答前做多少 reasoning 的旋钮。更高 effort 花更多 output token，换难题上更高的胜率。
aliases:
  - Reasoning effort
  - Thinking effort
---

effort（努力度）是控制 [model](./Model.md)（模型）回答前做多少 reasoning（推理）的旋钮。按 [model provider request](./Model%20provider%20request.md)（模型提供商请求）设置，它控制模型在开始写出你看到的回复之前，思考进行多长。那段思考和其他一切一样在 [inference](./Inference.md)（推理）时生成；[harness](./Harness.md)（运行框架）常把它藏起来，但那是模型在做的真实工作。

更高的 effort 花钱更多、跑得更慢。reasoning 以 [tokens](./Token.md)（词元）形式吐出，即便你从未见到也按 [output tokens](./Output%20tokens.md)（输出 token）计费，并且一次一个 token 生成——所以调高 effort 拉长答案到达前的等待，也加到账单上。权衡是更多深思对速度与成本。

多数 harness 把 effort 暴露成一个小阶梯：

| 档位 | 用途 |
| ------ | ---------------------------------------------------------------------- |
| Low    | 机械编辑、查资料、路径唯一且规格清楚的改动。 |
| Medium | 日常编码——通常是默认值。 |
| High   | 难缠的 bug、设计决定、多步计划。 |
| Max    | 最难的问题，答错代价高昂、难以挽回。 |

设法设错的症状是双向的。难题上把 effort 设太低，你会得到自信而浅薄的答案，跳过了问题所需的推理——读起来没问题，却错在日后要你付出代价的地方。为一行重命名设成 max，你就得干等一段长思考，其产出最低档也不会少。

让 effort 匹配任务，不匹配 [session](./Session.md)（会话）。真正难推理的部分调高，周围例行的工作调低。

_用法：_

"它老搞砸这个并发修复——我已经重新解释三遍了。"

"把 effort 调高。那是 reasoning 密集的 bug，默认档下它在选定方案前想得不够久。"
