---
layout: default
title: "Horizon Summary: 2026-10-17 (ZH)"
date: 2026-10-17
lang: zh
---

> 从 181 条内容中筛选出 10 条重要资讯。

---

**科技新闻**
1. [Claude 将 NIST ECDSA 曲线种子追溯到 lrand48](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenBSD 37 年老内核漏洞的利用分析](#item-tech-news-2) ⭐️ 8.0/10
3. [越狱 PS5 上原生运行 llama.cpp 与 GGUF 模型](#item-tech-news-3) ⭐️ 7.0/10
4. [JPEG XL 与 AVIF 的 Web 场景对比及编码速度权衡](#item-tech-news-4) ⭐️ 7.0/10
5. [研究称美国 90% 工时任务缺乏 AI 基准覆盖](#item-tech-news-5) ⭐️ 7.0/10

**全球要闻**
1. [霍尔木兹海峡附近船只遇袭报告创新高，石油出口放缓](#item-world-news-1) ⭐️ 7.0/10
2. [巴西亚马逊毁林降至 1988 年来最低，总统决选成关键](#item-world-news-2) ⭐️ 7.0/10
3. [Starlink access still not fully restored for Ukraine’s military, says Zelenskyy](#item-world-news-3) ⭐️ 7.0/10
4. [特朗普称美海军封锁已阻止伊朗船只穿越霍尔木兹海峡](#item-world-news-4) ⭐️ 7.0/10
5. [乌克兰在顿涅茨克推进，特朗普被指给普京柴油交易](#item-world-news-5) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Claude 将 NIST ECDSA 曲线种子追溯到 lrand48](https://www.anthropic.com/research/ecdsa-curve-origins) ⭐️ 8.0/10

Anthropic 公布的研究称，Claude 找到了 NIST P-192、P-224、P-256、P-384 和 P-521 五条 ECDSA 曲线种子的来源：它们并非哈希算法输出，而是 C 库 lrand48 随机数生成器以 Unix 时间戳为种子生成的。这为长期未获解释的曲线种子出处问题提供了一个具体答案，但该结论仍属 Anthropic 的单方研究结果，并非独立验证。第五个二进制种子 B-163 仍未匹配任何已尝试的生成方式，社区评论推测它可能与其他种子同法生成、只是在发布过程中被误输了一位数字。

hackernews · ahlCVA · 10月16日 18:55 · [社区讨论](https://news.ycombinator.com/item?id=50122800)

**「背景」** NIST 的 ECDSA 曲线（P-192、P-224、P-256、P-384、P-521）在标准中公布了所谓“种子”值，本意是让外界能够验证曲线参数并非为隐藏后门而特意挑选。长期以来的常见猜测是这些种子来自对某个固定短语的哈希，但此前无人能复现该推导。Anthropic 于 2026 年 10 月 16 日发布的文章称，Claude 发现这些种子来自以 Unix 时间戳播种的 C 库 lrand48，而非哈希算法输出；评论同时指出，B-163 仍无法用同样方法解释。

**「对使用者与标准信任的影响」** 对依赖 NIST P-192/P-224/P-256/P-384/P-521 的开发者与合规团队而言，这一发现不构成更换曲线或迁移密钥的理由：种子早已是公开常量，弄清它们由 lrand48 加 Unix 时间戳生成，并不改变已发布曲线的密码强度或实现兼容性。它的实际后果是削弱了长期基于「种子来源不明、可能被刻意构造」的对 NIST 曲线的信任质疑，但并未给出全面澄清——评论者指出，确认生成方式无法排除当年通过遍历时间戳挑选特定曲线的可能，而第五个二进制种子 B-163 仍无解释（有人推测可能是发布途中的录入错误），因此在 B-163 说明清楚之前，不宜把它当作对所有相关曲线来源的完整结论。

**「社区讨论」** 有评论者指出，确认种子由 lrand48 生成只能说明生产方式，不能证明曲线未被刻意挑选：如果搜索时间戳，仍有可能从被丢弃的候选中选出具有特定性质的曲线。另有评论认为，B-163 无法匹配最简单的解释是发布时数字被误输，而非存在另一套未知生成方法。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.explainx.ai/blog/claude-ecdsa-nist-curve-seeds-lrand48-anthropic-frontier-red-team-backdoor-question-2026">ECDSA Curve Seeds Solved: Claude Found lrand48 (2026 ...</a></li>
<li>Claude reveals ECDSA curve origins - Anthropic</li>

</ul>
</details>

**标签**: `#cryptography`, `#AI-assisted research`, `#NIST standards`, `#random number generation`, `#security`

---

<a id="item-tech-news-2"></a>
### [OpenBSD 37 年老内核漏洞的利用分析](https://calif.io/research/big-fish) ⭐️ 8.0/10

安全研究网站 calif.io 发布了一篇针对 OpenBSD 内核漏洞的利用分析文章，称该漏洞已在代码中存续 37 年。随附的分析摘要指出，文章不仅描述利用过程，还讨论了此类漏洞为何能在长期代码审查与审计中存活。但本次提供的材料仅有标题、分析摘要与社区评论，原文并未给出，因此漏洞的具体位置、受影响版本、触发条件以及是否已修复均无法从现有信息中确认，关于“37 年”的说法目前只是文章自身的表述。

hackernews · rs\_rs\_rs\_rs\_rs · 10月16日 14:44 · [社区讨论](https://news.ycombinator.com/item?id=50118977)

**「背景」** 这篇研究涉及的是 OpenBSD 中一个约 37 年前从旧 BSD 代码继承下来的内核漏洞；外部报道称 Calif 的研究展示了如何借此取得超级用户（root）权限（tool-1-2）。内核中这类长期潜伏的缺陷并非孤例：有报道称，AI 辅助分析也曾在 OpenBSD 中找到一个长达 23 年的 use-after-free，说明成熟并经长期维护的代码仍可能藏有未被发现的漏洞（tool-1-3）。

**「影响与处置」** 对运行 OpenBSD 7.9 且存在不受信任本地账户的机器（如共享 shell 主机、多用户服务器），该漏洞链可把本地权限提升为 root；现有证据展示的是本地概念验证，并未表明可远程直接利用。因此实际处置重点是收紧本地账户权限并跟踪官方勘误，现有工具结果尚未明确说明哪一版本包含修复，是否已发布补丁需以 OpenBSD 官方公告为准。

**「社区讨论」** 评论者 phendrenad2 指出，该漏洞似乎是在 1999 年 8 月 NetBSD 重写相关代码时被顺带修复的。ozereray1 则提出一个争论点：这类漏洞是否真能靠模糊测试或静态分析发现，还是必须由人从利用原语的角度思考才能识别，评论中并未就此形成一致结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://dzen.ru/a/atJi8f5wA2igUvxy">Calif получила root в OpenBSD через 37 -летнюю ошибку ядра | Дзен</a></li>
<li><a href="https://cloudnews.tech/ai-is-finding-os-bugs-at-a-new-scale-and-linux-is-feeling-the-pressure/">AI Is Finding OS Bugs at a New Scale, and Linux Is... | Cloud News</a></li>
<li>Researchers Demonstrate OpenBSD Root Exploit Chaining 37-Year-Old ...</li>
<li>OpenBSD: 37-year-old kernel bug allowed root takeover | iMasters</li>
<li>Big Fish: Exploiting a 37-Year-Old Kernel Bug in OpenBSD | daily.dev</li>

</ul>
</details>

**标签**: `#OpenBSD`, `#kernel security`, `#vulnerability exploitation`, `#operating systems`, `#security research`

---

<a id="item-tech-news-3"></a>
### [越狱 PS5 上原生运行 llama.cpp 与 GGUF 模型](https://github.com/cobanov/PS5LM) ⭐️ 7.0/10

GitHub 项目 PS5LM 称可在越狱 PS5 上原生运行 llama.cpp，并加载 GGUF 模型；其前提是主机已越狱，面向的是 homebrew 与硬件破解用户，而非普通零售固件用户。当前提供的材料没有给出性能基准、兼容模型列表、内存占用或支持的量化格式等细节，因此只能确认这是一条可行的本地推理路径，不能确认其在不同 GGUF 模型上的实际速度与稳定性。该项目出现在 Hacker News 讨论中，关注点是把消费级游戏主机改作本地 LLM 推理硬件。

hackernews · Anon84 · 10月16日 18:32 · [社区讨论](https://news.ycombinator.com/item?id=50122431)

**「背景」** llama.cpp 是支持 GGUF 格式模型的开源推理引擎，此前已被社区移植到多种非标准硬件与平台上，而 PS5 默认处于锁闭状态、需先越狱才能运行自制程序。据 Reddit 上一位 fork 作者的说法，这类移植通过 Vulkan（RADV 移植）在 PS5 的 GPU 上原生运行 llama.cpp，应用可用内存约 11.4 GiB；另有介绍文章称 PS5LM 可把主机变成提供 OpenAI 与 Anthropic 接口的本地服务器。以上均为第三方描述，项目本身未随附基准测试数据。

**「影响」** 该方案只对已越狱的 PS5 有效，普通用户无法直接复现，项目本身也未给出基准数据；对想在同一代定制 APU 上跑本地推理的人，更容易获得的替代路径是 AMD BC-250 矿板——tool-3-1 的配置指南给出用 Ollama 推理时平均 52W、峰值 119W 的功耗，tool-3-2 的 Reddit 讨论报告在 Qwen 35B MoE 上约 38 tok/s。评论区提到的“2 bit 量化运行 Qwen 27B”等性能数字和每日约 70 美分电费属于个人经验，未经来源或独立验证，实际部署前应自行测量。

**「社区讨论」** 评论者一方面担心把项目主要托管在 GitHub 上可能被索尼下架，建议改用自有域名；另一方面有评论称，即便只能以 2 bit 量化运行 Qwen 3.8 27B，约 70 美分/天的功耗也足以支撑服务器错误监控、安防画面审查等长时任务，但这些性能与成本数字来自评论者说法，未在材料中验证。还有评论认为同类思路可能适用于 BC250 等基于裁剪版 PS5 芯片的矿板，并把 LLM 驱动的 NPC 视为游戏中的潜在应用。

<details><summary>参考链接</summary>
<ul>
<li>Vaibhav Sisinty on X: &quot;Someone just jailbroke a PS5 and got a 27B AI ...</li>
<li>Qwen 27B at ~20 tok/s on a jailbroken PS5&#x27;s GPU. I forked PS5LM ... - Reddit</li>
<li>PS5LM: llama.cpp on a Jailbroken PS5 (55 tok/s, 2026) | explainx.ai Blog</li>
<li>GitHub - akandr/bc250: AMD BC-250 (PS5 APU) setup guide — Ollama + ...</li>
<li>Did anyone tried to use AMD BC-250 for inference? : r/LocalLLaMA - Reddit</li>

</ul>
</details>

**标签**: `#llama.cpp`, `#PS5 homebrew`, `#GGUF inference`, `#local AI`, `#hardware hacking`

---

<a id="item-tech-news-4"></a>
### [JPEG XL 与 AVIF 的 Web 场景对比及编码速度权衡](https://jakearchibald.com/2026/jpeg-xl-vs-avif/) ⭐️ 7.0/10

Jake Archibald 发表了一篇针对 Web 使用场景的 JPEG XL 与 AVIF 对比文章（2026 年 10 月 16 日）。文章的核心议题是编码速度与压缩体积之间的权衡，Hacker News 讨论补充了具体编码器参数：有评论者指出 libjxl 的最高 effort 只能把照片再压小 2–7%、把截图和插画再压小约 25%，却要耗时 9–46 秒，是默认设置的 50–180 倍，而 jixel 可在数秒内得到相同结果。另一位评论者给出了生成 AVIF 的 ffmpeg 命令，声称可将体积缩小到十分之一以上并保留 PNG 透明度。包括 ezst 在内的部分评论者认为，两个格式都尚未成熟，不宜把任何“胜出”结论当作定论。

hackernews · farlight · 10月16日 16:12 · [社区讨论](https://news.ycombinator.com/item?id=50120224)

**「背景」** JPEG XL 与 AVIF 都是被拿来替代传统 JPEG 的 Web 图像格式，二者的取舍集中在压缩率、编码速度以及编码器与浏览器工具链的成熟度上。Jake Archibald 的这篇对比正是围绕这些取舍展开，具体涉及 libjxl 的 effort 等级设置、AVIF 在 ffmpeg 下的参数选择，以及高压缩时画质细节是否被“合理地”抹平。评论中也有从 MP3/LAME 的多年调优历史出发的观点，认为两种格式都还需要时间打磨，目前不宜把任何“胜出”结论当作定论。

**「对 Web 图片投放的实际影响」** 对需要选定图片投放格式的 Web 开发者而言，当前可行路径仍是把 AVIF（或 WebP）作为主格式并保留 JPEG 回退：外部对比显示 AVIF 已有约 93% 的浏览器支持，而 JPEG XL 的支持仍属实验性、覆盖约 10–25% 的用户，Chrome 145 也只是以标志位形式提供 JPEG XL，尚不足以作为主力格式投放。编码端同样存在代价需要权衡：评论指出 libjxl 在最高 effort 下相对默认设置仅让照片体积缩小 2–7%，却慢 50–180 倍，因此有人建议改用 jixel 或按 AVIF 的 ffmpeg 参数调优来压缩流水线时间。

**「社区讨论」** 争论焦点在于现在是否值得采用：Metricon 给出了生产环境可用的 AVIF ffmpeg 设置并称体积可缩小 10 倍以上，PaulHoule 则以一张 F1 图片中赛车高光被“看似合理的内容”取代为例，质疑 AVIF 的质量取舍；ezst 借 MP3/LAME 和 WebP 的历史提醒，两个编解码器都还需要时间打磨，现在不宜宣判胜负。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.inverity.ai/posts/avif-vs-webp-vs-jpeg-xl-2026">AVIF vs WebP vs JPEG XL in 2026: Which Format Wins?</a></li>
<li><a href="https://coretoolshub.com/blog/avif-vs-webp-vs-jpeg-xl-2026/">AVIF vs WebP vs JPEG XL — 2026 Format Comparison</a></li>

</ul>
</details>

**标签**: `#image codecs`, `#web performance`, `#AVIF`, `#JPEG XL`, `#browser tooling`

---

<a id="item-tech-news-5"></a>
### [研究称美国 90% 工时任务缺乏 AI 基准覆盖](https://www.mercor.com/research/labor-index/benchmark-map/) ⭐️ 7.0/10

Mercor 的 Labor Index 研究将美国劳动工时与现有 AI 基准的任务覆盖范围做映射，结论是约 90% 的美国工作小时花在现有基准“很少覆盖或完全没有覆盖”的任务上。该分析还称，即便控制了 AI 暴露度，工资总额更大的职业所对应的 O\*NET 任务在基准提示中仍被显著过度代表。这些是该商业研究机构自身基于 O\*NET 的映射分析结论，而非独立的模型能力测量；“覆盖良好”的具体判定标准在评论中受到质疑。

hackernews · speckx · 10月16日 17:08 · [社区讨论](https://news.ycombinator.com/item?id=50121179)

**「背景：基准覆盖如何测算」** Mercor 的 Benchmark Map 把 29 个公开的 agentic AI 基准映射到 O\*NET 职业任务分类中的 923 个职业，并称这些基准只覆盖 18,797 个 O\*NET 任务中的 924 个。O\*NET 将职业拆解为具体任务，因此该映射成为“90% 美国工时缺少基准覆盖”这一估算的基础。

**「对评估与部署的影响」** 对依赖公开基准判断模型能否接手具体工作的开发者与组织而言，Mercor 把 29 个 AI 基准映射到 923 个职业，并称其只覆盖 18,797 个 O\*NET 任务中的 924 个，据此估计约 90% 的美国工作小时落在几乎没有基准覆盖的任务上；这意味着现有基准分数不能直接外推到未覆盖岗位，团队若要做部署评估，需要针对自身任务补充内部或领域专用评测。该结论来自 Mercor 的映射和估算，尚非独立验证。

**「社区讨论」** 评论者 OtherShrezzing 认为原文把“覆盖良好”当作“有任何覆盖”来用，并举例称“社会工作者与照护—就子女养育问题为家长提供咨询”这一类别仅因有 13 条提示就被判为“覆盖良好”，因此质疑该覆盖度指标是否经得起严格定义。legitster 则以鲍莫尔成本病作类比，称自己编码与脚本效率提高约 20 倍后，时间反而被演示、Jira、QA 等任务填满；armcat 援引 Karpathy 的说法，称 AI 目前实际只处理约 2-5% 的工作。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.mercor.com/research/labor-index/benchmark-map/">A benchmark map of the US economy | Mercor</a></li>
<li><a href="https://runtimewire.com/article/mercor-benchmark-map-human-work-thesis">Mercor estimates 90% of US work hours lack AI benchmark coverage</a></li>
<li><a href="https://www.explainx.ai/blog/mercor-benchmark-map-90-percent-us-working-hours-not-covered-ai-benchmarks-2026">AI Benchmark Coverage: 90% of US Work Is Unmeasured ...</a></li>
<li><a href="https://www.mercor.com/research/labor-index/benchmark-map/">A benchmark map of the US economy | Mercor</a></li>
<li><a href="https://runtimewire.com/article/mercor-benchmark-map-human-work-thesis">Mercor estimates 90% of US work hours lack AI benchmark coverage</a></li>
<li><a href="https://www.explainx.ai/blog/mercor-benchmark-map-90-percent-us-working-hours-not-covered-ai-benchmarks-2026">AI Benchmark Coverage: 90% of US Work Is Unmeasured ...</a></li>

</ul>
</details>

**标签**: `#AI benchmarks`, `#AI evaluation`, `#labor market impact`, `#O\*NET`, `#workforce automation`

---

## 全球要闻

<a id="item-world-news-1"></a>
### [霍尔木兹海峡附近船只遇袭报告创新高，石油出口放缓](https://www.bbc.co.uk/news/articles/cmde8dpg8g0no?at_medium=RSS&amp;at_campaign=rss) ⭐️ 7.0/10

BBC 事实查核（BBC Verify）对英国海事机构数据的分析显示，过去一周在霍尔木兹海峡附近有 12 艘船只遭到袭击，为有记录以来的单周最高数字。报道同时称，同期石油出口放缓。报道未披露袭击由何方实施、遇袭船只的国籍或类型、人员伤亡情况，也未提供经确认的出口降幅数字。相关数据来自英国海事机构，属于该机构的统计记录，尚不清楚是否有其他机构独立核实。

rss · BBC World · 10月16日 05:00

**「背景」** 此前，霍尔木兹海峡自 2026 年 10 月 10 日起对商业航运实际关闭，10 月 4 日仅 4 艘船通过，远低于正常约 85 艘/日的水平，布伦特油价为 104.72 美元（tool-2-1）。据报告，10 月 11 日单日发生六起袭击，为冲突开始以来最高单日总数，截至 10 月 16 日当周又报告了四起额外袭击（tool-2-2）。另据记录，9 月 28 日至 10 月 5 日期间，霍尔木兹海峡周边至少发生 12 起涉及油轮、LNG 或 LPG 船只的袭击、未遂袭击或骚扰事件，商品船流量降至两个多月来最低（tool-2-3）。

**「对航运与石油外运的影响」** 目前的直接影响集中在航运安排与原油外运节奏上，而不是供应中断。BBC 事实查核依据英国海事机构数据的统计称，一周内 12 艘船只遭袭；与此同时，《纽约时报》援引 TankerTrackers 的数据报道，10 月以来经相关路线每日仍外运约 500 万桶原油，若把管道与海峡流量合计，本月中东每天约有 1700 万桶原油离港。运营层面的调整已在发生：Rigzone 报道称，伊拉克计划增租油轮，至少两艘将在未来数日内抵达，以加强对经霍尔木兹海峡运油的掌控。CNBC 将袭击的密集化归因于伊朗试图压制原油出口的回升，称油轮&quot;几乎每日&quot;遇袭——这属于媒体的归因性报道，并非已确认结论。接下来值得关注的是袭击频次是否维持在高位，以及上述外运量能否延续。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://straits.live/">Strait of Hormuz Closed, Day 224 | Live Tracker &amp; Monitor</a></li>
<li><a href="https://southfront.press/iran-reports-tanker-fire-as-hormuz-ship-attacks-hit-wartime-record-video/">Iran Reports Tanker Fire as Hormuz Ship Attacks Hit Wartime Record...</a></li>
<li><a href="https://www.echemi.com/cms/3260974.html">Hormuz Sees at Least 12 Vessel Incidents in One Week as... | ECHEMI</a></li>
<li><a href="https://www.nytimes.com/2026/10/15/business/hormuz-oil-tanker-attacks.html">Gulf Oil Is Still Flowing Despite a Surge in Attacks on Ships</a></li>
<li><a href="https://www.rigzone.com/news/wire/tankers_sought_as_iraq_pushes_on_with_hormuz_oil_exports-06-oct-2026-184778-article/?rss=true">Tankers Sought as Iraq Pushes On with Hormuz Oil Exports | Rigzone</a></li>
<li><a href="https://www.cnbc.com/2026/10/09/iran-war-strait-hormuz-tanker-attack-oil.html">Tanker attacks in Strait of Hormuz surge to wartime high</a></li>

</ul>
</details>

**标签**: `#Strait of Hormuz`, `#Maritime security`, `#Oil exports`, `#Shipping attacks`, `#Middle East`

---

<a id="item-world-news-2"></a>
### [巴西亚马逊毁林降至 1988 年来最低，总统决选成关键](https://www.theguardian.com/environment/2026/oct/16/brazil-amazon-deforestation-lowest-on-record-election) ⭐️ 7.0/10

巴西政府最新数据显示，巴西亚马逊地区的森林砍伐量已降至 1988 年开始记录以来的最低水平。报道称，这对卢拉而言是一项成功，他正面临 10 月 25 日的总统决选。该报道指出，这一成果能否维持还是会被逆转仍悬而未决，因为两位候选人对雨林未来以及雨林如何影响特朗普执政下的美国关系持截然不同立场。

rss · The Guardian World · 10月16日 19:37

**「背景」** 据美国协会/美洲理事会（AS/COA）的投票追踪，2026 年 10 月 4 日巴西总统选举首轮投票中，参议员弗拉维奥·博索纳罗（Flávio Bolsonaro）以 47%的得票率位居第一，卢拉得票 45.2%，两人均未达到避免进入第二轮所需的 50%，因此定于 10 月 25 日举行决选；poliwave 的实时结果页面同样列出这一首轮得票分布。本轮决选因此成为决定现任总统卢拉所推动的亚马逊保护政策能否延续的直接条件。

**「影响与关注点」** 这一创纪录的降幅能否维持，取决于 10 月 25 日的总统决选。据《卫报》报道，进入决选的两名候选人对雨林未来以及在美国总统特朗普治下如何处理对美关系持有截然不同的主张。Mother Jones 的报道称，如果弗拉维奥·博索纳罗保持其在首轮投票中建立的优势，将给亚马逊雨林带来不利前景；可关注 10 月 25 日决选结果，以及此后巴西环境执法力度是否随之调整。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.as-coa.org/articles/poll-tracker-brazils-2026-presidential-election">Poll Tracker: Brazil&#x27;s 2026 Presidential Election | AS/COA</a></li>
<li><a href="https://www.poliwave.com/br/live/presidente-2026">Brazil Presidential Runoff 2026 Live Results - poliwave.com</a></li>
<li><a href="https://www.theguardian.com/environment/2026/oct/16/brazil-amazon-deforestation-lowest-on-record-election">Brazilian Amazon deforestation falls to lowest on record as pivotal...</a></li>
<li><a href="https://www.motherjones.com/politics/2026/10/flavio-bolsonaros-brazils-election-victory-runoff-lula-climate-amazon-deforestation/">Flávio Bolsonaro’s Advance in Brazil ’s Election Is Grim News for the...</a></li>

</ul>
</details>

**标签**: `#Brazil`, `#Amazon deforestation`, `#climate change`, `#Brazil presidential election`, `#environmental policy`

---

<a id="item-world-news-3"></a>
### [Starlink access still not fully restored for Ukraine’s military, says Zelenskyy](https://www.theguardian.com/world/2026/oct/16/ukraine-military-starlink-access-starshield-volodymyr-zelenskyy) ⭐️ 7.0/10

Zelenskyy says Ukraine’s military Starlink access is still not fully restored amid reports the White House ordered restrictions, while asking EU leaders for an additional €70bn in defence funding.

rss · The Guardian World · 10月16日 18:01

**标签**: `#Ukraine`, `#Starlink`, `#US foreign policy`, `#EU defence funding`, `#Russia-Ukraine war`

---

<a id="item-world-news-4"></a>
### [特朗普称美海军封锁已阻止伊朗船只穿越霍尔木兹海峡](https://www.aljazeera.com/news/liveblog/2026/10/17/draft-2?traffic_source=rss) ⭐️ 7.0/10

半岛电视台 10 月 17 日的一则实时博客条目称，美国总统特朗普表示，美国海军的封锁已阻止所有伊朗船只穿越霍尔木兹海峡。这是特朗普的单方面说法，该条目未给出封锁的开始时间、执行方式或其他行动细节，也没有独立核实、第三方航运数据或美方官方文件的佐证。截至该条目发布，霍尔木兹海峡实际的船只通行状况无法从这一来源得到确认。

rss · Al Jazeera · 10月17日 00:00

**「背景」** 不列颠百科全书关于 2026 年伊朗战争的条目记载，美国与伊朗（连同以色列）于 4 月 7 日至 8 日达成初步停火，但此后数周冲突转向美伊之间围绕霍尔木兹海峡通行受限的博弈。美国外交关系委员会的文章则指出，美国曾在当地实施海上封锁并攻击伊朗船只，伊朗则布设水雷并多次关闭海峡。

**「影响与后续观察」** 特朗普称美国海军封锁已阻止所有伊朗船只穿越霍尔木兹海峡。若这一单方面说法被证实，直接后果将落在经该海峡的能源运输上：美国能源信息署将霍尔木兹海峡称为全球最重要的石油运输咽喉，正常条件下每日约 2100 万桶石油经此通过，约占全球石油消费的 20%、海运石油贸易的 25%（tool-3-1、tool-3-2）；另有航运分析称，在本轮危机导致通行中断前，该海峡是全球运量最大的能源运输通道（tool-3-3）。目前尚无独立核实，后续可关注油轮追踪与航运流量数据是否显示实际中断，以及美伊双方是否给出官方确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.cfr.org/articles/strait-hormuz-us-iran-maritime-flash-point">The Strait of Hormuz : A U . S .- Iran Maritime Flash Point | Council on...</a></li>
<li><a href="https://www.britannica.com/event/2026-Iran-war">2026 Iran war | Oil, Explained, United States , Israel, Strait of Hormuz ...</a></li>
<li><a href="https://straits.live/what-percentage-of-world-oil-passes-through-the-strait-of-hormuz">What Percentage of World Oil Passes Through the Strait of ...</a></li>
<li><a href="https://www.eia.gov/todayinenergy/detail.php?id=61002">The Strait of Hormuz is the world&#x27;s most important oil ...</a></li>
<li><a href="https://www.speedcommerce.com/insights/how-much-of-the-worlds-shipping-goes-through-the-strait-of-hormuz/">How Much of the World’s Shipping &amp; Oil Goes Through the ...</a></li>

</ul>
</details>

**标签**: `#Iran`, `#Strait of Hormuz`, `#US Navy`, `#blockade`, `#Trump`

---

<a id="item-world-news-5"></a>
### [乌克兰在顿涅茨克推进，特朗普被指给普京柴油交易](https://www.aljazeera.com/news/2026/10/16/ukraine-repels-russian-forces-as-us-support-wavers-energy-strikes-escalate?traffic_source=rss) ⭐️ 7.0/10

据半岛电视台 2026 年 10 月 16 日报道，乌克兰在顿涅茨克州开展的代号“维瓦尔第行动”中，据称收复了更多被俄罗斯占领的领土，BBC 记者随乌军行动进行了报道。报道称，在同一周内，美国总统特朗普被指站在俄罗斯一边，并向普京提供了一项柴油交易。报道还提到，乌方乐观情绪因与美国关系恶化而受到抑制。上述内容来自该报道的表述，行动规模、领土收复的具体范围以及柴油交易的具体条款均未在现有信息中说明，也未获独立证实。

rss · Al Jazeera · 10月16日 17:28

**「背景」** 乌克兰于 2026 年 9 月中旬正式宣布发动“维瓦尔第行动”（Operation Vivaldi），在顿涅茨克州北部莱曼（Lyman）一带夺回部分领土，并打乱了俄军向当地若干要塞城市的推进。据《基辅独立报》报道，乌军第三军团称，截至 10 月 14 日，乌方在顿涅茨克州莱曼方向又夺回 101 平方公里。

**「后续影响」** 这项柴油协议于 10 月 9 日由特朗普宣布，他称俄罗斯将向全球市场供应逾 400 万吨柴油（CNBC）。CNN 报道称，该协议在美国国会遭到两党批评，有议员警告此举违反旨在制裁俄罗斯的联邦法律。CNBC 汇总的报道还引述专家观点，认为协议可能削弱西方对俄经济施压与协调；Forbes 则指出该协议不太可能压低柴油价格。接下来值得观察的是国会是否推动立法阻止协议落地，以及协议能否按宣布的规模执行。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://theconversation.com/operation-vivaldi-success-of-ukraines-counteroffensive-shows-it-has-learned-to-manoeuvre-on-a-drone-filled-battlefield-294197">Operation Vivaldi: success of Ukraine’s counteroffensive ...</a></li>
<li><a href="https://kyivindependent.com/ukraine-war-latest-operation-vivaldi-liberates-another-101-square-kilometers-in-donetsk-oblast/">Ukraine war latest: Operation Vivaldi liberates another 101 ...</a></li>
<li><a href="https://www.cnn.com/2026/10/11/politics/us-russia-diesel-deal-bipartisan-criticism">Trump’s US-Russia diesel deal draws bipartisan criticism - CNN</a></li>
<li><a href="https://www.cnbc.com/2026/10/09/trump-putin-diesel-russia-sanctions-ukraine.html">Trump-Putin diesel deal contradicts Russia sanctions law ... Trump strikes deal with Putin to supply Russian diesel to U.S ... Trump throws Putin another lifeline with diesel deal Trump’s diesel deal with Putin drives a wedge through the ... Trump’s Russian Diesel Deal, Explained - Council on Foreign ... Trump-Putin Diesel Deal Unlikely To Reduce Prices - Forbes</a></li>
<li><a href="https://www.cnbc.com/2026/10/09/trump-putin-russian-diesel-us-global-markets.html">Trump strikes deal with Putin to supply Russian diesel to U.S ... Trump throws Putin another lifeline with diesel deal Trump’s diesel deal with Putin drives a wedge through the ... Trump’s Russian Diesel Deal, Explained - Council on Foreign ... Trump-Putin Diesel Deal Unlikely To Reduce Prices - Forbes</a></li>

</ul>
</details>

**标签**: `#Ukraine war`, `#Donetsk`, `#US-Russia relations`, `#Trump-Putin`, `#Energy deal`

---