## 一个简单的技巧，大幅提升 ChatGPT 翻译质量

ChatGPT 3.5 是免费使用的，因此本文主要测试了 ChatGPT 3.5 的翻译技巧。虽然 ChatGPT 3.5 的能力比 ChatGPT 4 弱很多，但如果你有 ChatGPT 4，可以参考相关技巧，效果会更好！以下是一些实用的 prompt 示例，供大家尝试。

---

### ChatGPT 3.5 的参考 prompt

> 你是一位专业中文翻译，擅长英译中翻译，并且擅长对翻译结果进行二次修改和润色成通俗易懂的中文。我希望你能帮我将以下英文段落直译翻译成中文，而后根据直译结果重新意译和润色。

#### 规则：
- 这些字幕包含机器学习或 AI 等专业知识相关，注意翻译时术语的准确性；
- 保留特定的英文术语、数字或名字，并在其前后加上空格，例如：“生成式 AI 产品”，“不超过 10 秒”；
- 首先按照字面意思直译翻译这一段文本内容；
- 然后基于直译结果重新意译，意译时务必对照原始英文，不要添加也不要遗漏内容，并以让翻译结果通俗易懂，符合中文表达习惯。

---

### 英文原文示例

> Yeah, I will talk about large-language models in 2025. Why do we need that suffix in 2025? What we call large is misleading in that large models of today will be small models only in a few years. Along with the change in the perception of scale, many insights, observations, and conclusions we make along the way with the current large-language models will be outdated. And in some cases, invalidated. Fortunately, insights based on church principles or that are fundamental tend to stay relatively longer than the advanced ideas that look so fancy. In this talk, I would like to share such fundamental ideas that I have observed working in the field for the past four years, and mostly by observing some of the brightest minds that I'm fortunate to have interacted with. My hope is that whatever I talk about today is fundamental enough that it stays relevant at least for a few years. Let's get started. There's one unique aspects of large language models, and that is some abilities only emerge at certain scale. And this makes really important to just have a different perspective in viewing all this field. So here's what l mean. Details don't matter here. X-axis is some scale. You can think of it as a model parameter count, training data, training compute, whatever. You just think about some scale. Y-axis is also not that important. Some performance metrics of the task that you care about. And we have seen over and over this kind of pattern where small models just don't have any chance of solving it, 0% or random guessing. And at some scale, suddenly the models solve this task, and sometimes very well. And this kind of phenomenon, we call it an emergence, a phase change like sudden emergence of this capability. And this is very unique for this large language models. And I think this brings many important perspectives change for AI researchers.

---

### 直译结果

在 2025 年，我将谈论大型语言模型。为什么我们需要在 2025 年加上这个后缀呢？我们所谓的“大型”可能会误导，因为今天的大型模型在未来几年可能仅仅被视为小型模型。随着对规模感知的变化，我们与当前大型语言模型一同获得的许多见解、观察和结论将会过时，有些情况下甚至会被推翻。幸运的是，基于基本原则或根本性的见解通常比那些看起来很花俏的先进思想更具持久性。在这次演讲中，我想分享一些我在过去四年在这一领域中观察到的基本思想，大部分是通过与我有幸互动的一些最聪明的头脑。我希望今天我所谈论的内容足够基本，至少能在未来几年保持相关性。让我们开始吧。大型语言模型有一个独特之处，那就是一些能力只在特定规模下才会显现出来。这使得以不同的角度来看待这一领域变得非常重要。这就是我所说的。细节并不重要。X 轴代表某种规模，可以将其视为模型参数数量、训练数据、训练计算等等。只要考虑某种规模即可。Y 轴也不那么重要，代表了您关心的任务的某些性能指标。我们一次又一次地看到这种模式，其中小型模型根本没有解决这个任务的机会，成功率为 0% 或纯属随机猜测。而在某个规模下，突然之间，模型能够解决这个任务，有时做得非常出色。我们称这种现象为“出现”或“阶段性改变”，就像这种能力的突然出现一样。而这对于大型语言模型来说是非常独特的。我认为这给 AI 研究者带来了许多重要的视角变化。

---

### 意译和润色后

2025 年，我将探讨大型语言模型。为什么要特别强调“2025”呢？所谓的“大型”其实可能具有误导性，因为今天被称为“大型”的模型，几年后可能就只能算“小型”了。随着我们对规模的认知不断变化，许多基于当前大型语言模型的见解、观察和结论可能会逐渐过时，甚至在某些情况下被推翻。然而，基于基本原则或核心理念的见解往往比那些看似先进但稍纵即逝的想法更具持久性。在这次演讲中，我将分享过去四年中我在这一领域观察到的一些核心理念，这些理念大多来自与一些顶尖人才的交流和合作。我希望今天分享的内容足够基础，能够在未来几年内依然具有参考价值。

大型语言模型有一个独特的特性：某些能力只有在达到特定规模时才会显现。这使得我们需要从不同的视角来审视这一领域。让我来解释一下。具体细节并不重要。X 轴可以代表模型参数数量、训练数据量或计算量等任何与规模相关的指标。Y 轴则代表某些任务的性能指标。我们反复观察到这样一种模式：小型模型几乎无法完成某些任务，成功率接近 0% 或仅仅是随机猜测。然而，当模型达到某个规模时，突然就能很好地完成这些任务。这种现象被称为“能力涌现”或“阶段性变化”，即某种能力的突然显现。这种现象是大型语言模型的独特之处，也为 AI 研究者提供了许多新的视角。

---

### ChatGPT 4 的参考 prompt

#### 复杂版
> 你是一位精通简体中文的专业翻译，我希望你能帮我将以下英文视频字幕翻译成中文。

#### 精简版
> 你是一位精通简体中文的专业翻译，曾参与《纽约时报》和《经济学人》中文版的翻译工作，因此对于新闻和时事文章的翻译有深入的理解。

---

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

---

特别说明：本文仅供学习交流，如有不妥欢迎后台联系小编。

**- END -**

原文作者：王真真