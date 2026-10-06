---
layout: default
title: "Horizon Summary: 2026-10-06 (ZH)"
date: 2026-10-06
lang: zh
---

> 从 240 条内容中筛选出 5 条重要资讯。

---

**科技新闻**
1. [Polars 2.0 正式发布](#item-tech-news-1) ⭐️ 8.0/10
2. [Reflection 发布 501B 总参数开放权重模型 Beam](#item-tech-news-2) ⭐️ 8.0/10
3. [Mistral 发布 1 万亿参数 Mistral Large 4 预览版](#item-tech-news-3) ⭐️ 8.0/10
4. [Gleam 的 Erlang 后端改为输出 Erlang 抽象形式](#item-tech-news-4) ⭐️ 7.0/10
5. [Dust 声称可无需反向传播预训练 Transformer](#item-tech-news-5) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Polars 2.0 正式发布](https://pola.rs/posts/release-polars-2/) ⭐️ 8.0/10

Polars 2.0 已发布，这是该开源 DataFrame 库的大版本更新，面向使用 Polars 进行数据处理与分析的开发者。现有材料没有给出该版本的具体新功能、性能数字或兼容性说明，因此无法核实相对上一版本的实际变化。社区评论显示 2.0 在此前已有候选版本（rc），有用户表示会在发布当晚升级到正式版，并有人将该发布帖视作包含性能基准的博文。

hackernews · simicd · 10月6日 11:59 · [社区讨论](https://news.ycombinator.com/item?id=49977177)

**「背景」** Polars 是用 Rust 编写的开源 DataFrame 库，常与 pandas、DuckDB、PyArrow 一同出现在数据处理工具的讨论中。Polars 官方博客在 2026 年 9 月 2 日发布了 2.0 的首个候选版本（RC），当时表示正式版将在随后几周内推出，并且 2.0 并不打算做成一次大规模功能更新。

**「影响」** 发布材料中的 SQL 基准是在 AWS c7a.4xlarge（16 vCPU、32GB 内存）和 c7a.metal（192 vCPU、384GB 内存）上，对照 DuckDB 1.5.6、DuckDB 2.0.0.dev2610011535 与 DataFusion 54.0.0 测得的，因此这些数字只对应特定硬件规格和特定对手版本；团队在把生产工作负载迁到 Polars 2.0 前应先用自身数据与机器复现，而不宜直接套用公告里的相对性能结论。

**「社区讨论」** 一位自称做过基准测试（包括 TPC 基准）的评论者提醒，这类发布博文不应被解读为“数据库 A 比数据库 B 快 X%”，因为影响因素太多，更合理的理解是团队集中做了性能优化、预期某些工作负载会快于上一版本。另有评论者询问 Polars 是否已成为 Pandas 的完整替代、两者各自更适合什么场景，还有人提到面向 Claude 的技能包似乎尚未更新。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://pola.rs/posts/announcing-polars-2/">Polars — Pre-release of Polars 2.0</a></li>
<li><a href="https://pola.rs/posts/release-polars-2/">Polars — Release of Polars 2.0</a></li>

</ul>
</details>

**标签**: `#Polars`, `#DataFrame`, `#Open Source`, `#Performance Benchmarks`, `#Data Engineering`

---

<a id="item-tech-news-2"></a>
### [Reflection 发布 501B 总参数开放权重模型 Beam](https://reflection.ai/blog/introducing-beam) ⭐️ 8.0/10

Reflection 发布了 Beam，这是一个总参数 5010 亿、激活参数 230 亿的开放权重稀疏 MoE 模型，面向编码、推理和智能体工作负载。社区转述的模型说明称，Beam 使用 23.8 万亿个来自网络与授权专有数据集的 token 预训练，并匹配或超过同类规模开放基础模型；演示还称它在复现一个几天前才出现的谜题任务上达到 95.5% 覆盖率，介于 Opus 5 的 92.5% 与 Fable 之间。上述性能、训练数据和泛化结果目前均来自 Reflection 的介绍或社区转述，尚无独立验证，具体许可证与权重获取方式也未在现有材料中说明。

hackernews · Philpax · 10月5日 19:16 · [社区讨论](https://news.ycombinator.com/item?id=49969183)

**「背景」** Beam 是 Reflection 发布的首个开放权重模型，此前该公司并未推出过开放权重版本。稀疏 Mixture-of-Experts（MoE）架构的关键在于：每个 token 只激活总参数中的一小部分，因此总参数量会明显大于单次推理实际参与计算的参数量，这也是该模型以 5010 亿总参数搭配 230 亿激活参数发布的前提概念。

**「影响」** 对打算自托管或以 Beam 为基础构建产品的开发者而言，最直接的限制是权重尚未放出：第三方报道称 Reflection 计划在 2026 年 10 月晚些时候以 Apache 2.0 许可发布权重，在此之前只能依赖其 API，部署与许可决策需要等到该版本落地。同时已有第三方将它按 API 成本与基准得分同 DeepSeek V4.1 Flash 等模型并列比较，并标注部分结果尚未得到独立验证，因此现阶段不宜把厂商公布的对比当作选型依据。

**「社区讨论」** 评论者欢迎更多开放权重模型，但有评论者对演示的泛化说法表示怀疑，并指出该谜题是几天前才出现的，95.5% 覆盖率只把它放在 Opus 5 与 Fable 之间。另有评论者认为选择模型时发布方比当前基准更重要，质疑 Reflection 能否长期存在；还有人把 Beam 与 DeepSeek V4.1 Flash 对比，列出 552B 总参数、8B 预填激活、16B 解码激活、196B N-gram/PLE 参数与 Beam 的 501B 总参数、23B 激活、无 N-gram/PLE 参数等差异。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://reflection.ai/blog/introducing-beam">Introducing Beam : Reflection ’s 501 B open - weight model — Reflection</a></li>
<li><a href="https://www.unite.ai/reflection-ai-unveils-beam-a-501b-parameter-open-weight-model/">Reflection AI Unveils Beam , a 501 B -Parameter Open - Weight Model</a></li>
<li><a href="https://www.datacamp.com/blog/reflection-ai-beam">Beam : Reflection AI &#x27;s 501 B Open - Weight Model | DataCamp</a></li>
<li><a href="https://benchlm.ai/compare/deepseek-v4-1-flash-vs-reflection-beam">DeepSeek V4.1 Flash vs Beam: Benchmarks &amp; Cost | BenchLM.ai</a></li>
<li><a href="https://www.explainx.ai/blog/reflection-ai-open-weight-model-us-answer-deepseek-qwen-october-2026">Reflection Beam: 501B Open-Weight Model, Benchmarks ...</a></li>
<li><a href="https://www.thinkfacility.com/blog/reflection-beam-open-weight-model-501b/">Reflection&#x27;s first open-weight model, Beam, has 501 billion ...</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#mixture-of-experts`, `#large language models`, `#AI model release`, `#agentic AI`

---

<a id="item-tech-news-3"></a>
### [Mistral 发布 1 万亿参数 Mistral Large 4 预览版](https://x.com/MistralAI/status/2107457414387622310) ⭐️ 8.0/10

Mistral 于 10 月 6 日发布 1 万亿参数的 Mistral Large 4（代号“le Chonk”），称其为全球最强开源模型之一，但目前仅面向开发者、网络安全负责人及政府机构预览，计划本月晚些时候扩大开放。该模型重点面向网络安全、编程、制造、金融和多模态任务，Mistral 称其使用 4000 个英伟达 Grace Blackwell GPU 训练两个月。Mistral 同时承认该模型在编程等领域仍落后于前沿模型。

telegram · zaihuapd · 10月6日 14:02

**「背景：万亿参数背后的 MoE 架构」** 理解这次发布的关键在于其架构：Mistral Large 4 采用细粒度混合专家（MoE）设计，总参数 1.05 万亿，但每个 token 仅激活约 490 亿参数，并配有 1.6B 的视觉编码器，因此同时具备多模态能力（tool-2-2）。Mistral 将其定位为开放权重的通用多模态模型，并计划随后公开发布权重，目前先以公开预览形式提供（tool-2-1、tool-2-2）。

**「影响」** 由于目前仅限预览，大多数开发者和企业尚无法直接部署 Mistral Large 4；而官方承认其在编程等任务上落后于前沿模型，意味着对编码性能要求高的团队可能仍需依赖其他模型，关注网络安全或欧洲替代方案的用户则可能等待其本月晚些时候扩大开放。

**「社区讨论」** 社区评论中，有用户认为 Mistral 在经历 Large 3 的挫折后仍留在竞争中，并引用数据称该模型在网络安全（CyberGym-E2E 82%）和视觉接地（Dense 200 42%，略高于 GPT-6 Astra 的 41%）上表现突出。但同一评论也指出其综合 Vals Index（48.05%）低于 GLM-5.3（53.51%）且单次测试成本更高（13.78 美元 vs 7.25 美元）；另有用户报告推理设置仅有“none”和“high”两档，且 high 并未带来明显更长的输出。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://venturebeat.com/technology/mistral-debuts-large-4-le-chonk-a-1-trillion-parameter-text-output-model-with-high-benchmarks-planned-for-open-weights-release">Mistral debuts Large 4 &#x27;Le Chonk&#x27;, a 1-trillion parameter text output ...</a></li>
<li><a href="https://docs.mistral.ai/models/mistral-large-4-0">Mistral Large 4 - Mistral AI | Mistral Docs</a></li>

</ul>
</details>

**标签**: `#Mistral`, `#large language models`, `#open-source AI`, `#Nvidia hardware`, `#model release`

---

<a id="item-tech-news-4"></a>
### [Gleam 的 Erlang 后端改为输出 Erlang 抽象形式](https://gleam.run/news/gleam-doesnt-compile-to-erlang-source-anymore/) ⭐️ 7.0/10

Gleam 项目的公告称，其编译器的 Erlang 代码生成器已不再输出 Erlang 源码，而是直接生成 Erlang abstract forms（Erlang 编译器使用的 AST 表示）。公告表示 Giacomo Cavalieri 在过去几个月里完全重写了这一生成器，新设计在结构与输出格式上都与旧版不同；Elixir 同样以 abstract forms 作为编译目标，Erlang 的 parse transform 也在这一表示上操作。评论者提醒，标题容易让人误以为 Gleam 不能再编译出 Erlang 可用的产物，但变化只涉及中间输出格式，目标仍是 BEAM 生态。上述细节来自公告标题、社区引述与分析摘要，所给材料未包含公告全文。

hackernews · ingve · 10月6日 08:08 · [社区讨论](https://news.ycombinator.com/item?id=49975619)

**「背景」** Erlang abstract forms 是 Erlang 编译器使用的 AST 表示，由 Erlang terms 构成，标准库中提供了操作该表示的例程；Elixir 也是经由 abstract forms 编译到 Erlang，而非直接生成源码（tool-2-2）。2024 年 10 月的 gleam-lang/gleam 讨论 \#3705 曾提出把 Gleam 的编译目标从 Erlang 源代码改为 Erlang abstract format，理由是更可靠的实现以及与 BEAM 及其既有工具更好的集成（tool-2-3）。Gleam 官方公告将这一方向与 BEAM 字节码对比，指出字节码并非固定不变，因此选择了 abstract forms（tool-2-2）。

**「对下游工具链的影响」** 这项改动意味着，任何依赖 Gleam 输出 Erlang 源码文本的下游流程——例如检查生成的 .erl 文件、对生成的源码做后处理或自定义构建步骤——都需要改为面向 Erlang abstract forms 来操作，否则可能失效（Gleam 仍然编译到 BEAM，改变的只是中间表示）。abstract forms 正是 Erlang 编译器与 parse transform 所使用的 AST 表示，因此基于源码文本的转换逻辑将不再直接适用。

**「社区讨论」** 有评论者指出标题有误导性，并引述公告原文说明改动只是从生成 Erlang 源码变为生成 abstract forms，Gleam 依然能产出 Erlang 可用的结果；另一位评论者解释 abstract forms 是 Erlang 编译器的 AST 表示，由 Erlang term 构成、标准库提供了便于操作的例程，Elixir 也编译到该表示。还有评论者表示希望 Gleam 未来能像 Rust 或 Go 那样编译到原生目标，也有人感谢 Giacomo Cavalieri 的直播对 Gleam 与 Rust 特性的讲解。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://gleam.run/news/gleam-doesnt-compile-to-erlang-source-anymore/">Gleam doesn&#x27;t compile to Erlang source anymore</a></li>
<li><a href="https://github.com/gleam-lang/gleam/discussions/3705">Compile to Erlang abstract format · gleam-lang gleam ...</a></li>
<li><a href="https://www.erlang.org/docs/18/apps/erts/absform.html">Erlang -- The Abstract Format</a></li>
<li><a href="https://www.cosmiclearn.com/erlang/parse-transform.php">Erlang Parse Transform - cosmiclearn.com</a></li>

</ul>
</details>

**标签**: `#Gleam`, `#Erlang`, `#compiler backend`, `#BEAM`, `#programming languages`

---

<a id="item-tech-news-5"></a>
### [Dust 声称可无需反向传播预训练 Transformer](https://qlabs.sh/research/dust) ⭐️ 7.0/10

研究项目 Dust 发布文章，声称能够在不使用反向传播的情况下预训练 Transformer，其思路属于零阶（无导数）优化。该页面未提供可核实的实验结果、模型规模或算力数据，因此目前只能视为一项方法主张，而非已展示的能力。Hacker News 上的相关帖子获得 251 分和 68 条评论，讨论集中在这类方法是否真的可行。

hackernews · E-Reverance · 10月5日 21:15 · [社区讨论](https://news.ycombinator.com/item?id=49970871)

**「背景」** 零阶（无导数）优化不计算梯度，而是通过扰动参数、观察损失变化来估计下降方向；长期以来它在大型神经网络训练中远慢于反向传播。该项目页面称 Dust 是首个在预训练 transformer 语言模型上与反向传播具有竞争力的零阶方法，并称其比权重空间进化策略（weight-space ES）高效数个数量级。项目同时放出了最小实现仓库，用前向评估加 SGD 训练 transformer，保留了论文的估计器与调参默认值，但省略了完整实验中的执行优化。

**「实际影响」** 由于该研究帖没有给出可验证的结果或规模数据，目前有据可查的零阶优化落地场景仍集中在反向传播本身不适用的领域，例如用零阶方法微调不可微的脉冲神经网络，以及在图 Transformer 上做零阶优化实验；这些属于微调或特定结构，而非大规模预训练。因此对打算在 Transformer 预训练中替换反向传播的团队而言，更稳妥的做法是先把这类方法当作黑箱或不可微目标下的补充手段，等出现可复现的扩展性结果后再评估其替代可能。

**「社区讨论」** 评论者普遍持怀疑态度：有人认为无导数优化每隔几年就会被重新炒作，但神经网络的目标函数通常是光滑的或满足 Lipschitz 条件，梯度能直接指明改进方向，而随机试探方向的做法会随参数量增加而收益递减；也有评论者认为零阶方法不应被当作反向传播的替代品，而更适合反向传播本身较弱的场景，并举例提到用中心差随机梯度估计（CD-RGE）在不做时间反向传播的情况下训练大型 RNN 的工作。另有评论者质疑《苦涩的教训》式论证是否适用于零阶方法，认为一旦损失函数被平滑化、去除非凸性因素，Dust 宣称相对一阶方法的优势可能消失，并指出两者受同一经验风险最小化框架约束。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://qlabs.sh/research/dust">Dust: Pretraining Transformers Without Backpropagation - qlabs.sh</a></li>
<li><a href="https://github.com/qlabs-eng/dust/tree/main/">GitHub - qlabs-eng/dust</a></li>
<li><a href="https://www.ijcai.org/proceedings/2025/0348.pdf">Sharpness-aware Zeroth - order Optimization for Graph Transformers</a></li>
<li><a href="https://arxiv.org/html/2608.21223">Event-triggered Implicit Perturbation for Zeroth - Order Fine-Tuning of...</a></li>

</ul>
</details>

**标签**: `#transformers`, `#backpropagation`, `#zeroth-order optimization`, `#pretraining`, `#machine learning`

---