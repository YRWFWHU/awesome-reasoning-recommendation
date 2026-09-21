# Awesome Reasoning for Recommendation

**推理增强推荐：思维链、潜在推理、强化学习与推理时扩展。**

精选论文、官方实现与评测资源，围绕三个问题组织：**推理了什么？推理有效吗？成本是多少？**

[入门路线](#start-here) · [论文清单](#papers) · [近期必读](#frontier) · [前沿地图](docs/frontier-map.md) · [方法对照](docs/method-matrix.md) · [证据卡片](docs/frontier-reading.md) · [基准选型](docs/benchmarks.md) · [参与贡献](CONTRIBUTING.md)

**最近整理：2026-09-21** · 97 篇文献：74 篇核心方法、6 项基准、7 篇评测研究、1 篇综述、9 篇背景 · 17 篇精选卡片

## 收录范围

关注推理如何参与推荐决策，包括显式文本思维链、潜在状态迭代、结构化路径搜索、推理蒸馏、奖励学习，以及智能体的工具选择与交互规划。

- **核心方法**：推理用于偏好理解、物品选择、排序、重排或交互决策。
- **评测资源**：检验推荐推理、约束满足、证据使用及决策可靠性。
- **综述导航**：连接研究方向与问题，和新方法分别计数。
- **相关背景**：生成式检索、物品编码及推荐目标对齐，单列为阅读前置。

使用 LLM、强化学习或生成物品 ID，本身不足以说明具备推荐推理能力。仅在结果产生后补充解释的工作，需另行说明与决策的关系。这里的分类是仓库的编辑约定。

### 如何阅读条目

- 日期采用 **arXiv 首次提交月份**；`arXiv` 表示来源，不表示论文一定未经同行评审。不统一标注未经独立核实的会议录用信息。
- 每篇论文只维护一个完整条目，按主要贡献归类，其他联系用标签和交叉链接表达。
- 普通条目已核实一手摘要与提交记录；精选卡片另核对方法、实验或成本章节。详细来源见 [核实记录](docs/sources.md)。
- “官方代码”表示链接归属与仓库页面已核实；“未核实”不等于“未开源”。**本仓库尚未开展论文实验复现。**

<a id="start-here"></a>
## 入门路线

| 想了解什么 | 建议顺序 | 阅读时带着的问题 |
| --- | --- | --- |
| 生成式推荐如何获得推理能力 | [TIGER](#paper-tiger) → [OneRec-Think](#paper-onerec-think) → [OneReason](#paper-onereason) | 物品语义如何接入语言推理？ |
| 如何用强化学习优化推荐推理 | [RecZero / RecOne](#paper-reczero) → [GR2](#paper-gr2) → [SAPO](#paper-sapo) | 奖励优化的是最终结果，还是具体推理步骤？ |
| 增加推理计算能做什么 | [ReaRec](#paper-rearec) → [TTR](#paper-ttr) → [PROMISE](#paper-promise) | 增加的是隐状态迭代、验证还是搜索？ |
| 潜在推理怎样发展 | [LatentR³](#paper-latent-r3) → [FLR](#paper-flr) → [LaRec](#paper-larec) → [HiLaR](#paper-hilar) | 连续状态怎样初始化、分工和获得监督？ |
| 潜在推理怎样与 SID 交叉 | [S²GR](#paper-s2gr) → [LASAR](#paper-lasar) → [IBA](#paper-where-reasoning-matters)；对照 [Latte](#paper-latte)、[BARGE](#paper-barge) | 表示结构、连续计算和离散搜索如何共同影响效果？ |
| 如何控制推理成本 | [WhisperRec](#paper-whisperrec) → [EvoReason](#paper-evoreason) → [rEDMRec](#paper-redmrec) → [SelfDR](#paper-selfdr) | 蒸馏进入参数、潜在状态，还是外部记忆？ |
| 如何自适应分配计算 | [DTRec](#paper-dtrec) → [ManCAR](#paper-mancar) → [EGLR](#paper-eglr) → [IBA](#paper-where-reasoning-matters) | 停止条件、列表位置和总预算怎样控制？ |
| 如何评估推理价值 | [评测指南](docs/evaluation.md) → [τ-Rec](#paper-tau-rec) → [RPCBench](#paper-rpcbench) | 排名准确之外，约束与证据是否可靠？ |

### 术语速查

| 术语 | 本仓库中的含义 |
| --- | --- |
| CoT（思维链） | 在最终选择或预测前生成中间分析步骤 |
| SFT（监督微调） | 用示例训练模型，可包含推理轨迹与最终结果 |
| RL（强化学习） | 用奖励优化模型行为；需进一步说明奖励与推理的关系 |
| TTS（推理时扩展） | 在预测阶段增加或分配计算预算，如多步迭代、搜索和验证 |
| 潜在推理 | 在隐状态或潜在 token 中进行计算，不必生成自然语言理由 |
| Semantic ID（语义 ID） | 用离散编码表达物品语义；生成这类编码与生成文字思维链需区分 |

<a id="frontier"></a>
## 前沿阅读导航

本页连接编码结构、逐步潜在推理、路径搜索和推理蒸馏。以下按研究问题选读；完整的控制实验建议见 [8 个研究方向](docs/frontier-map.md)。

| 近期入口 | 为什么读 | 证据边界 |
| --- | --- | --- |
| [NarraLite](#paper-narralite)、[P³Rec](#paper-p3rec) · 2026-09 | 潜在未来语义与先验/后验偏好监督 | 非个性化续集和个性化推荐须分开比较 |
| [LIGE-GR · 2026-09](#paper-lige-gr) | 未来价值引导列表搜索 | 更宽 beam 的收益与价值目标变化需隔离 |
| [SelfDR · 2026-09](#paper-selfdr) | 用推理自蒸馏支持直接预测 | 需计入教师与训练成本 |
| [RPCBench · 2026-09](#paper-rpcbench) | 推荐前先诊断错误前提 | 裁判评分和程序化验证不同 |
| [UPR 画像干预 · 2026-09](#paper-transparent-upr) | 检查偏好表示的变化是否改变排序 | 局限于所测评分回归模型与候选协议 |
| [Disconnect · 2026-08](#paper-disconnect) | 检查轨迹质量与决策效果是否一致 | 单基座、三个领域的控制实验 |
| [rEDMRec · 2026-08](#paper-redmrec) | 推理知识进入可编辑记忆 | 冻结学生，20 候选排序 |
| [CRS 协议研究 · 2026-08](#paper-crs-protocol) | 候选、计分和解码会改变模型比较 | 未单独隔离 CoT 贡献 |
| [EvoReason](#paper-evoreason)、[LaRec](#paper-larec)、[HiLaR](#paper-hilar) · 2026-07 | 潜在轨迹的对齐、演化与逐层监督 | 组件收益不等于语义忠实性 |
| [IBA · 2026-07](#paper-where-reasoning-matters) | 固定预算下按 SID 位置分配计算 | 不同于自然语言 CoT 扩展 |

**深入使用：** [方法与证据矩阵](docs/method-matrix.md) · [12 篇前沿证据卡](docs/frontier-reading.md) · [5 篇基础阅读卡](docs/reading-notes.md) · [6 个基准选型表](docs/benchmarks.md)。

本轮检索截止与重叠窗口见 [2026-09-21 周检记录](notes/weekly-search-2026-09-21.md)；历史记录保留在 [总体检索](notes/frontier-search-2026-09-15.md) 与 [潜在推理更新](notes/latent-reasoning-update-2026-09-17.md)。

<a id="papers"></a>
## 论文清单

- [思维链与推理学习](#cot)（7）
- [潜在推理与偏好表示](#latent)（18）
- [强化学习与奖励设计](#rl)（9）
- [推理时扩展与自适应预算](#tts)（15）
- [推理蒸馏与效率](#distillation)（15）
- [交互与智能体推荐](#agents)（10）
- [评测、基准与有效性证据](#benchmarks)（13）
- [综述与研究路线](#surveys)（1）
- [相关背景](#background)（9）

<a id="cot"></a>
## 思维链与推理学习

<a id="paper-onereason"></a>
### OneReason Technical Report

**2026-06 · arXiv · 进行中的技术报告** · `CoT` `SFT` `RL` `物品语义对齐`

通过物品语义感知、三层推荐思维链和分阶段强化学习增强推荐推理；同时研究 thinking 与 non-thinking 的差异，适合追问推理收益究竟来自训练还是预测阶段。

[论文](https://arxiv.org/abs/2606.06260) · [阅读卡片](docs/reading-notes.md#onereason) · 官方代码：未核实

<a id="paper-sidreasoner"></a>
### SIDReasoner: Reasoning over Semantic IDs Enhances Generative Recommendation

**2026-03 · arXiv** · `序列推荐` `语义ID` `CoT` `GRPO`

增强语义 ID 与语言的多任务对齐，再通过推理激活和基于预测结果的 GRPO 优化推荐推理；奖励依据 SID 正确前缀与物品有效性，不能直接视为自然语言推理步骤正确性评分。

[论文](https://arxiv.org/abs/2603.23183) · [官方代码](https://github.com/HappyPointer/SIDReasoner)

<a id="paper-onerec-think"></a>
### OneRec-Think: In-Text Reasoning for Generative Recommendation

**2025-10 · arXiv** · `序列推荐` `CoT` `GRPO` `物品语义对齐`

先对齐物品与文本语义，再学习推荐推理轨迹并用推荐奖励优化，使文本推理参与后续物品生成。

[论文](https://arxiv.org/abs/2510.11639) · [ACL 2026 正式版](https://aclanthology.org/2026.acl-long.123/) · [官方代码](https://github.com/wangshy31/OneRec-Think) · [阅读卡片](docs/reading-notes.md#onerec-think)

<a id="paper-gream"></a>
### GREAM: Generative Reasoning Recommendation via LLMs

**2025-10 · arXiv** · `语义ID` `CoT` `课程学习` `SRPO`

通过协同语义对齐、合成思维链课程训练和稀疏奖励优化，支持直接物品生成与先推理再推荐两种模式；两种模式的评测指标需分别阅读。

[论文](https://arxiv.org/abs/2510.20815) · [官方代码](https://github.com/Indolent-Kawhi/GRRM) · [证据卡片](docs/frontier-reading.md#gream)

<a id="paper-r2rec"></a>
### R2Rec: Reason-to-Recommend: Using Interaction-of-Thought Reasoning to Enhance LLM Recommendation

**2025-06 · arXiv** · `交互图` `CoT` `SFT` `RL`

将用户—物品图中的交互链转为分步推理，用轨迹监督与强化学习训练模型，把协同交互信息引入推荐决策。

[论文](https://arxiv.org/abs/2506.05069) · 作者匿名代码入口当前返回 401，内容未核实（见 [来源记录](docs/sources.md#unavailable-resources)）

<a id="paper-thinkrec"></a>
### ThinkRec: Thinking-based recommendation via LLM

**2025-05 · arXiv** · `个性化推荐` `合成轨迹` `专家融合`

注入用户行为分析、偏好识别和目标判断的合成推理轨迹，再按用户特征融合专家，学习个性化推荐推理。

[论文](https://arxiv.org/abs/2505.15091) · [官方代码](https://github.com/Yu-Qi-hang/ThinkRec)

<a id="paper-exp3rt"></a>
### EXP3RT: Review-driven Personalized Preference Reasoning with Large Language Models for Recommendation

**2024-08 · arXiv** · `评分预测` `重排` `评论` `CoT` `蒸馏`

从评论中提取偏好、构建画像，并蒸馏逐步评分推理，使用户与物品的匹配分析先于评分输出。

[论文](https://arxiv.org/abs/2408.06276) · [官方代码](https://github.com/jieyong99/EXP3RT)

<a id="latent"></a>
## 潜在推理与偏好表示

连续状态如何初始化、分解和接受监督是本类的主线；预算控制另见 [推理时扩展](#tts)，轨迹压缩另见 [推理蒸馏](#distillation)。

<a id="paper-narralite"></a>
### NarraLite: Efficient Multimodal Generative Recommendation with Latent Narrative Reasoning

**2026-09 · arXiv** · `多模态` `潜在推理` `语义ID` `叙事续集预测`

压缩视觉上下文，并路由连续潜在 token，以训练期的未来语义对齐引导续集 SID 生成。任务是用户无关的短剧剧情延续，不是个性化偏好预测；预测时潜在 token 并行处理，不生成文字思维链。

[论文](https://arxiv.org/abs/2609.16070) · 官方代码：未核实

<a id="paper-recgpt-v3"></a>
### RecGPT-V3：RecGPT-V3 Technical Report

**2026-07 · arXiv** · `工业推荐` `潜在推理` `SID` `记忆`

以持续更新的用户记忆连接文本标签与 SID，并把显式意图分析压缩为可学习潜在 token；需分别核算记忆维护、训练与在线推理成本。

[论文](https://arxiv.org/abs/2607.15591) · 官方代码：未核实

<a id="paper-recrec"></a>
### RecRec：RecRec: Latent Interests Recursive Reasoning for Sequential Recommendation

**2026-07 · arXiv** · `序列推荐` `潜在推理` `多兴趣`

将历史压缩为多个兴趣向量，在独立中间空间循环细化，再用于预测；通过深度监督支持调整推理步数，训练不依赖 RL。

[论文](https://arxiv.org/abs/2607.12945) · 官方代码：未核实

<a id="paper-hilar"></a>
### Hierarchical Latent Reasoning for LLM-based Recommendation（HiLaR）

**2026-07 · arXiv** · `层次偏好` `过程奖励`

按时间层次将偏好监督对齐到连续推理状态，以目标标题的平均 token 对数概率增益经裁剪、层级加权构造过程项；总奖励还包含冻结协同模型的偏好评分及层级对齐。输出为受目录约束的物品标题，不能将其用户偏好量化直接等同于物品 SID 解码。`潜在推理`

[论文](https://arxiv.org/abs/2607.27760) · [官方仓库（目前仅占位）](https://github.com/hupeiyu21/HiLaR)

<a id="paper-larec"></a>
### LaRec: Unleashing LLM-based Latent Reasoning for Generative Recommendation

**2026-07 · arXiv** · `轨迹对齐` `个性化探索`

将教师推理的步骤与方向对齐到潜在轨迹，再以用户历史引导的随机起点探索推理路径。`潜在推理`

[论文](https://arxiv.org/abs/2607.24617) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#larec)

<a id="paper-calir"></a>
### CaLIR：Beyond Matching: Category-Guided Latent Intent Reasoning for Generative Retrieval in E-Commerce

**2026-06 · arXiv** · `商品检索` `潜在推理` `SID`

在生成商品 SID 前执行类别引导的连续意图推理，结合多意图训练与查询相关前缀树。实验任务是电商搜索，不能直接视为序列推荐结论。

[论文](https://arxiv.org/abs/2606.07075) · 官方代码：未核实

<a id="paper-inturec"></a>
### Intuition-Guided Latent Reasoning for LLM-Based Recommendation（IntuRec）

**2026-06 · arXiv** · `候选先验`

先生成候选物品，再将候选转为偏好先验，初始化并引导后续潜在推理。`潜在推理`

[论文](https://arxiv.org/abs/2606.27684) · [官方代码](https://github.com/Ten-Mao/IntuRec)

<a id="paper-pauserec"></a>
### PauseRec: Implicit Reasoning for Large Language Model-based Generative Recommendation

**2026-06 · arXiv** · `潜在推理`

先预训练 pause token 连接语言与 SID 表示，再在物品预测前插入 pause 位置，仅用目标 SID 损失学习隐式计算；不要求文本理由监督。

[论文](https://arxiv.org/abs/2606.14142) · 官方代码：未核实

<a id="paper-lasar"></a>
### LASAR: Latent Adaptive Semantic Aligned Reasoning for Generative Recommendation

**2026-05 · arXiv** · `潜在推理` `语义ID` `自适应深度`

先学习 SID 语义，再引入循环隐状态反馈；以教师 CoT 的语义锚点约束潜在轨迹，并学习每个样本的推理深度。

[论文](https://arxiv.org/abs/2605.10207) · 官方代码：未核实

<a id="paper-flr"></a>
### Factorized Latent Reasoning for LLM-based Recommendation（FLR）

**2026-04 · arXiv** · `多兴趣` `GRPO`

用多个解耦偏好因子迭代细化潜在思考，并用正则化与 GRPO 对齐推荐目标。`潜在推理`

[论文](https://arxiv.org/abs/2604.26760) · [官方代码](https://github.com/ToAdventure/FLR)

<a id="paper-coderrec"></a>
### CoderRec: Cross-Scale Collaboration between LLMs and Lightweight Sequential Recommenders with Domain-Specific Latent Reasoning

**2026-03 · AAAI 2026 正式出版** · `潜在推理`

以轻量序列模型的表示作为领域潜在思考，使用跨规模模型协作与两阶段训练，将 LLM 的 SID 语义持续传递给下游推荐模型。

[论文](https://ojs.aaai.org/index.php/AAAI/article/view/38680) · 官方代码：未核实

<a id="paper-diffureason"></a>
### DiffuReason：DiffuReason: Bridging Latent Reasoning and Generative Refinement for Sequential Recommendation

**2026-02 · arXiv** · `序列推荐` `潜在推理` `扩散` `GRPO`

先用潜在思考形成意图假设，再通过扩散细化表示，并以 GRPO 联合对齐排名目标。

[论文](https://arxiv.org/abs/2602.09744) · 官方代码：未核实

<a id="paper-plr"></a>
### PLR：Parallel Latent Reasoning for Sequential Recommendation

**2026-01 · arXiv** · `序列推荐` `潜在推理` `并行计算`

用多个连续推理流探索用户偏好，以多样性正则和混合聚合整合结果；扩展的是推理宽度，而非只增加单条链的深度。

[论文](https://arxiv.org/abs/2601.03153) · 官方代码：未核实

<a id="paper-s2gr"></a>
### S²GR: Stepwise Semantic-Guided Reasoning in Latent Space for Generative Recommendation

**2026-01 · arXiv** · `潜在推理` `语义ID` `过程监督`

在每个 SID 码生成前插入潜在思考，用对应码本层次的语义分布监督中间状态，同时引入协同行为与码本均衡训练。

[论文](https://arxiv.org/abs/2601.18664) · 官方代码：未核实

<a id="paper-onepiece"></a>
### OnePiece: Bringing Context Engineering and Reasoning to Industrial Cascade Ranking System

**2025-09 · arXiv** · `工业召回与排序` `潜在推理` `过程监督`

将结构化偏好与场景上下文、分块潜在状态细化和基于用户反馈链的渐进多任务训练结合，应用于工业级召回与排序。属于潜在推理推荐，不将其等同于SID自回归生成。

[论文](https://arxiv.org/abs/2509.18091) · 官方代码：未核实

<a id="paper-latent-cross"></a>
### Latent Cross Reasoning：Bridging Search and Recommendation through Latent Cross Reasoning

**2025-08 · arXiv** · `序列推荐` `搜索行为` `潜在推理`

从搜索与推荐历史中形成兴趣表示，再迭代筛取对推荐有用的搜索证据；使用对比学习与强化学习对齐目标物品和排名。

[论文](https://arxiv.org/abs/2508.04152) · 官方代码：未核实

<a id="paper-lares"></a>
### LARES：LARES: Latent Reasoning for Sequential Recommendation

**2025-05 · arXiv** · `序列推荐` `潜在推理` `循环深度`

在每个循环步骤细化全部输入 token，结合轨迹与步骤对齐预训练、强化后训练扩展潜在计算深度。

[论文](https://arxiv.org/abs/2505.16865) · 官方代码：未核实

<a id="paper-latent-r3"></a>
### Reinforced Latent Reasoning for LLM-based Recommendation（LatentR³）

**2025-05 · arXiv** · `无CoT监督` `GRPO`

无需文本 CoT 监督，通过 SFT 初始化和改进 GRPO 学习连续潜在推理。`潜在推理`

[论文](https://arxiv.org/abs/2505.19092) · [官方代码](https://github.com/xuwenxinedu/R3)

<a id="rl"></a>
## 强化学习与奖励设计

<a id="paper-rporec"></a>
### RPORec: Reinforced Preference Optimization for Reasoning-Augmented Recommendations

**2026-05 · arXiv** · `物品检索` `CoT` `RL` `推荐头`

用思维链辅助推荐头学习，再利用推荐头的奖励优化语言模型推理，将中间分析与物品检索目标联系起来。

[论文](https://arxiv.org/abs/2605.21967) · 官方代码：未核实

<a id="paper-sapo"></a>
### SAPO: Step-Aligned Policy Optimization for Reasoning-Based Generative Recommendation

**2026-05 · arXiv** · `下一物品预测` `RL` `信用分配` `语义ID`

将思考块与对应语义 ID token 对齐，按步骤计算组相对优势，改善稀疏结果奖励下的推理信用分配。

[论文](https://arxiv.org/abs/2605.17648) · 作者代码地址当前返回 404，公开实现未核实（见 [来源记录](docs/sources.md#unavailable-resources)）

<a id="paper-rerec"></a>
### ReRec: Reasoning-Augmented LLM-based Recommendation Assistant via Reinforcement Fine-tuning

**2026-04 · arXiv** · `推荐助手` `RFT` `奖励塑形` `推理步骤信用分配`

将排名、查询匹配和偏好匹配结合为奖励，按推理片段估计优势，并动态安排训练难度，使复杂推荐请求的多步分析与推荐目标对齐。

[论文](https://arxiv.org/abs/2604.07851) · [官方代码](https://github.com/jiani-huang/ReRec)

<a id="paper-gr2"></a>
### GR2: Generative Reasoning Re-ranker

**2026-02 · arXiv** · `重排` `CoT` `SFT` `DAPO` `奖励设计`

结合语义 ID 训练、教师推理轨迹和 DAPO 优化候选重排，并针对保留原候选顺序的奖励投机设计条件奖励。

[论文](https://arxiv.org/abs/2602.07774) · [阅读卡片](docs/reading-notes.md#gr2) · 官方代码：未核实

<a id="paper-r2rank"></a>
### R2Rank: Reasoning to Rank: An End-to-End Solution for Exploiting Large Language Models for Recommendation

**2026-02 · arXiv** · `排名` `CoT` `PPO` `列表效用`

对每个用户—物品对单独推理与评分，再用 Plackett–Luce 排列代理将列表级推荐效用传回语言模型和评分头。

[论文](https://arxiv.org/abs/2602.12530) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#r2rank)

<a id="paper-reczero"></a>
### RecZero / RecOne: Think before Recommendation: Autonomous Reasoning-enhanced Recommender

**2025-10 · arXiv** · `评分预测` `CoT` `GRPO` `冷启动`

以用户分析、物品分析、匹配和评分组成结构化推理；比较直接强化学习的 RecZero 与先进行 SFT 冷启动的 RecOne。两者属于同一篇论文。

[论文](https://arxiv.org/abs/2510.23077) · [官方代码](https://github.com/AkaliKong/RecZero)

<a id="paper-mgfrec"></a>
### MGFRec: Towards Reinforced Reasoning Recommendation with Multiple Groundings and Feedback

**2025-10 · arXiv** · `多轮推理` `GRPO` `物品对齐` `用户模拟`

在推理过程中反复与真实物品空间对齐，结合用户智能体的模拟反馈及 GRPO 修正推荐推理；模拟反馈不等于真实用户在线反馈。

[论文](https://arxiv.org/abs/2510.22888) · 官方代码：未核实

<a id="paper-recllm-r1"></a>
### RecLLM-R1: A Two-Stage Training Paradigm with Reinforcement Learning and Chain-of-Thought v1

**2025-06 · arXiv** · `推荐列表` `CoT` `SFT` `GRPO` `多目标奖励`

先用用户历史与物品文本进行推荐 SFT，再以 GRPO 和多步思维链联合考虑准确性、多样性及业务目标。

[论文](https://arxiv.org/abs/2506.19235) · 官方代码：未核实

<a id="paper-r2ec"></a>
### R²ec: Towards Large Recommender Models with Reasoning

**2025-05 · arXiv** · `下一物品预测` `CoT` `双头模型` `RecPO`

在同一模型中分别生成推理链与预测物品，以融合奖励联合优化两者，减少独立推理模型与推荐器串联的开销。

[论文](https://arxiv.org/abs/2505.16994) · [官方代码与模型入口](https://github.com/YRYangang/RRec)

<a id="tts"></a>
## 推理时扩展与自适应预算

分别标注潜在状态迭代、候选验证和结构化路径搜索；训练数据或训练 FLOPs 扩展不自动归入 TTS。

<a id="paper-lige-gr"></a>
### LIGE-GR: A Smooth Leap from Ranking to Generative Recommendation in the LLM Era

**2026-09 · arXiv** · `列表推荐` `未来价值` `搜索` `工业推荐`

把列表前缀视为决策状态，通过继续观看概率和未来价值估计引导 Palette 束搜索，显式考虑当前选择对后续列表的影响。属于结构化决策搜索；其闭式未来价值估计不等同另训价值网络或文字 CoT。

[论文](https://arxiv.org/abs/2609.18148) · 官方代码：未核实

<a id="paper-epic"></a>
### EPIC: Explicit Posterior Item Conditioning for Semantic ID Diffusion Recommendation

**2026-09 · arXiv** · `语义ID` `结构化推断` `扩散`

在 SID 去噪过程中，利用近期交互形成可行候选物品的个性化后验，再将物品概率边缘化回未确定的编码位置，影响后续选择。收录为物品假设参与中间决策的结构化推断，不将其等同于连续潜在思维链。

[论文](https://arxiv.org/abs/2609.03522) · 官方代码：未核实

<a id="paper-rgd"></a>
### RGD：Reward Guided Decoding for Generative Recommendation

**2026-07 · arXiv** · `生成式推荐` `搜索` `奖励引导`

在 SID 解码期间用奖励模型调整路径概率，使高价值候选有机会在前缀阶段保留；固定生成器，通过测试时控制改变目标权重。

[论文](https://arxiv.org/abs/2607.25344) · 官方代码：未核实

<a id="paper-barge"></a>
### BARGE: Bridging the Structural Gap: Adapting Autoregressive Generation for Recommendation

**2026-07 · arXiv** · `结构化路径` `搜索` `语义ID`

通过物品边界感知编码、层级路径重排与正交双通道解码，缓解早期 SID 选错导致目标路径不可达的问题。归入结构化搜索，不视为连续潜在推理。

[论文](https://arxiv.org/abs/2607.21028) · 官方代码：未核实

<a id="paper-where-reasoning-matters"></a>
### Where Reasoning Matters: Rethinking Latent Reasoning in Semantic ID-based Generative Recommendation（IBA）

**2026-07 · arXiv** · `预算分配` `语义ID`

在固定总潜在步数下，根据位置的信息增益与预测收益分配语义 ID 的推理预算。`潜在推理`

[论文](https://arxiv.org/abs/2607.12425) · 官方代码：未核实

<a id="paper-v-star"></a>
### V-STAR：Spend Search Where It Pays: Value-Guided Structured Sampling and Optimization for Generative Recommendation

**2026-02 · arXiv** · `生成式推荐` `搜索` `RL`

选择有价值的分叉节点投入搜索预算，并利用兄弟分支间的奖励差异学习；研究概率主导解码与奖励目标不一致的问题。

[论文](https://arxiv.org/abs/2602.10699) · 官方代码：未核实

<a id="paper-thinking-hurts"></a>
### Why Thinking Hurts? Diagnosing and Rectifying the Reasoning Shift in Foundation Recommender Models

**2026-02 · arXiv** · `CoT` `语义ID` `对比解码`

分析显式理由生成中通用文本先验压过 SID 历史证据的现象，并用推理链压缩和偏差扣除的对比解码校正预测。

[论文](https://arxiv.org/abs/2602.16587) · 官方代码：未核实

<a id="paper-mancar"></a>
### ManCAR: Manifold-Constrained Latent Reasoning with Adaptive Test-Time Computation for Sequential Recommendation

**2026-02 · arXiv** · `序列推荐` `潜在推理` `协同图约束` `自适应停止`

用协同交互图构造意图先验并约束潜在推理轨迹，在相邻步骤的预测分布收敛后停止，控制漂移和过度计算。

[论文](https://arxiv.org/abs/2602.20093) · [官方代码](https://github.com/FuCongResearchSquad/ManCAR) · [证据卡片](docs/frontier-reading.md#mancar)

<a id="paper-promise"></a>
### PROMISE: Process Reward Models Unlock Test-Time Scaling Laws in Generative Recommendations

**2026-01 · arXiv** · `生成式推荐` `过程奖励` `束搜索` `结构化路径`

通过过程奖励评估层级语义 ID 的中间生成步骤，并引导测试时搜索。这里的推理对象是结构化生成路径，归入搜索与验证，不标为自然语言 CoT。

[论文](https://arxiv.org/abs/2601.04674) · 官方代码：未核实

<a id="paper-eglr"></a>
### EGLR: Reasoning While Recommending: Entropy-Guided Latent Reasoning in Generative Re-ranking Models

**2026-01 · arXiv** · `生成式重排` `潜在推理` `熵门控` `自适应预算` `GRPO`

在列表逐项生成过程中，根据当前决策熵插入数量可变的潜在推理 token，并用不同温度调节推理探索和物品选择。

[论文](https://arxiv.org/abs/2601.13533) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#eglr)

<a id="paper-dtrec"></a>
### DTRec: Learning Dynamic Reasoning Trajectories for Sequential Recommendation

**2025-12 · arXiv** · `序列推荐` `层级过程监督` `潜在推理` `自适应停止`

以逐渐细化的物品聚类原型监督中间状态，并综合预测熵、相邻预测一致性和隐状态变化学习何时停止推理。

[论文](https://arxiv.org/abs/2512.14036) · 官方代码：未核实

<a id="paper-mindrec"></a>
### MindRec: A Diffusion-driven Coarse-to-Fine Paradigm for Generative Recommendation

**2025-11 · arXiv** · `生成式推荐` `结构化推断` `掩码扩散` `搜索`

先生成层级类别，再按置信度补全 SID，并以扩散束搜索保留多条候选路径。结构化决策与搜索直接影响推荐结果；不将这种离散生成过程等同于连续潜空间推理。

[论文](https://arxiv.org/abs/2511.12597) · [官方代码](https://github.com/Mr-Peach0301/MindRec)

<a id="paper-reg4rec"></a>
### REG4Rec: Reasoning-Enhanced Generative Model for Large-Scale Recommendation Systems

**2025-08 · arXiv** · `生成式推荐` `搜索` `自我反思`

以并行量化构造无序语义 token 和多条推理路径，通过偏好奖励与一致性自检选择路径。其结构化语义推理与连续潜在状态迭代需要分别比较。

[论文](https://arxiv.org/abs/2508.15308) · 官方代码：未核实

<a id="paper-ttr"></a>
### TTR: Test-Time Scaling Strategies for Generative Retrieval in Multimodal Conversational Recommendations

**2025-08 · arXiv** · `商品检索` `多模态` `对话` `验证器` `重排`

根据对话理解当前意图，生成商品候选，再在预测阶段评价候选与意图的匹配程度以调整排序；增加的主要是候选验证计算。

[论文](https://arxiv.org/abs/2508.18132) · [阅读卡片](docs/reading-notes.md#ttr) · 官方代码：未核实

<a id="paper-rearec"></a>
### ReaRec: Think Before Recommend: Unleashing the Latent Reasoning Power for Sequential Recommendation

**2025-03 · arXiv** · `序列推荐` `潜在推理` `多步计算`

通过反复回馈序列末端隐状态细化用户表示，实现多步潜在推理。摘要中的 30%–50% 指事后分析上限，不应写成常规部署的平均提升。

[论文](https://arxiv.org/abs/2503.22675) · [官方代码](https://github.com/TangJiakai/ReaRec)

<a id="distillation"></a>
## 推理蒸馏与效率

<a id="paper-p3rec"></a>
### P³Rec: Distilling Prior–Posterior Preference Reasoning for LLM-based Recommendation

**2026-09 · arXiv** · `偏好推理` `蒸馏` `训练期推理`

把历史驱动的先验偏好和目标条件的后验偏好蒸馏到行为表示，再按兴趣熵校准检索方向。目标条件后验仅用于训练；预测仍需编码先验偏好，离线偏好生成与更新成本应单列。

[论文](https://arxiv.org/abs/2609.13993) · 官方代码：未核实

<a id="paper-trade-up"></a>
### Distill Globally, Adapt Locally: Reasoning Distillation and Product-Type Test-Time Training for Scalable Trade-Up Recommendation

**2026-09 · arXiv** · `商品关系` `理由蒸馏` `有监督适配`

把教师对商品升级替代关系的标签和理由蒸馏到轻量商品对分类器，再用每类带标签示例适配。在线只用预计算向量；任务是商品关系识别，PT-TTT 是按类型摊销的有监督适配。

[论文](https://arxiv.org/abs/2609.05363) · 官方代码：未核实

<a id="paper-lark"></a>
### LARK: Latent-Aligned Reasoning for Multimodal Recommendation

**2026-09 · arXiv** · `多模态推荐` `潜在推理` `CoT` `离线物品表示`

以视觉对齐和推理语义对齐缓解多步计算中的跨模态信息衰减；交替生成潜在状态与文本思维链，产出的物品表示可离线缓存供下游推荐使用。属于推理增强表示，不是在线 SID 自回归生成。

[论文](https://arxiv.org/abs/2609.04645) · 官方代码：未核实

<a id="paper-selfdr"></a>
### SelfDR: Self-Distillation from Reasoning for LLM-Based Recommendation

**2026-09 · arXiv** · `自蒸馏` `GRPO` `直接预测`

由同一基座构建推理器、带理由的教师和直接推荐学生，用下游奖励优化推理，再把教师预测分布蒸馏给学生。训练期利用理由，预测期直接推荐；需同时记录离线训练成本。

[论文](https://arxiv.org/abs/2609.03313) · [官方代码](https://github.com/JiangDeccc/SelfDistillation) · [证据卡片](docs/frontier-reading.md#selfdr)

<a id="paper-tgr"></a>
### TGR: Advancing Industrial Recommendation from Generative-Paradigm Ranking toward Unified Generation and Reasoning

**2026-09 · arXiv** · `工业推荐` `训练期推理` `语义ID`

其中 TGR-Reason 以目标首级 SID 监督训练期潜在状态，关闭 rollout（K=0）后离线导出完整 SID reason tokens，注入线上生成器。群体记忆检索是扩展设计，不属于正文表16的部署评测；训练、离线刷新和请求成本须分别核算。

[论文](https://arxiv.org/abs/2609.00986) · 官方代码：未核实

<a id="paper-redmrec"></a>
### rEDMRec: Distilling Large Language Model Reasoning into an Editable Experience Memory for Recommendation

**2026-08 · arXiv** · `冻结学生` `候选排序`

把教师推理存入可检索、可修改的外部经验记忆，供冻结学生排序；蒸馏对象是记忆，学生权重不更新。`记忆蒸馏`

[论文](https://arxiv.org/abs/2608.18952) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#redmrec)

<a id="paper-whisperrec"></a>
### WhisperRec: Latent Reasoning for Efficient Foundation Recommendation Models

**2026-07 · arXiv** · `CoT压缩` `潜在推理` `蒸馏`

将教师的多视角思维链压缩为可学习的潜在推理 token，结合对齐和课程式后训练，减少显式理由生成的开销。

[论文](https://arxiv.org/abs/2607.26621) · 官方代码：未核实

<a id="paper-evoreason"></a>
### EvoReason: Self-Evolving Reasoning Primitive-Guided On-Policy Distillation for Latent Reasoning in Generative Recommendation

**2026-07 · arXiv** · `在策略蒸馏` `推理原语`

将可复用推理操作引入教师，随学生轨迹进行在策略蒸馏，把显式推理压入潜在状态。`潜在推理`

[论文](https://arxiv.org/abs/2607.29010) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#evoreason)

<a id="paper-trialigngr"></a>
### TriAlignGR: Triangular Multitask Alignment with Multimodal Deep Interest Mining for Generative Recommendation

**2026-05 · arXiv** · `训练期推理` `CoT` `多模态` `SID`

在离散化前用思维链提取兴趣、融合图文信息，再以 SID、文本与视觉描述的多任务训练对齐。推理主要参与离线语义构建，不等同预测时增加思考步数。

[论文](https://arxiv.org/abs/2605.05249) · 官方代码：未核实

<a id="paper-momorec"></a>
### MoMoREC: A Multi-agent Motivation Generation Framework for Residual Semantic ID-Aware Recommendation

**2026-03 · AAAI 2026 正式出版** · `序列推荐` `动机推理` `语义ID` `训练期推理`

先用多智能体分析购物动机，再将对应连续表示压缩为残差语义 ID，供下游序列推荐器使用。推理发生在表示构建阶段，不是在线连续状态迭代。

[论文](https://ojs.aaai.org/index.php/AAAI/article/view/38623) · 官方代码：未核实

<a id="paper-isrf"></a>
### ISRF：Iterative Semantic Reasoning from Individual to Group Interests for Generative Recommendation with LLMs

**2026-03 · arXiv** · `生成式推荐` `语义推理` `训练期推理`

以多步属性推理构造物品语义和用户群体兴趣，再通过个体与群体信息的迭代优化改进推荐；应区分语义构建成本与预测成本。

[论文](https://arxiv.org/abs/2603.13934) · 官方代码：未核实

<a id="paper-deepinterestgr"></a>
### DeepInterestGR：DeepInterestGR: Mining Deep Multi-Interest Using Multi-Modal LLMs for Generative Recommendation

**2026-02 · arXiv** · `生成式推荐` `CoT` `多模态` `SID`

通过多模态模型的思维链挖掘兴趣，将兴趣信息写入物品离散编码，并用于监督微调与奖励设计。收录为预印本，未采用正文模板中的会议标注。

[论文](https://arxiv.org/abs/2602.18907) · 官方代码：未核实

<a id="paper-star"></a>
### STAR: Internalizing Multi-Agent Reasoning for Accurate and Efficient LLM-based Recommendation

**2026-02 · arXiv** · `轨迹蒸馏` `协同证据` `工具调用` `GRPO`

多智能体教师把协同行为转为文字证据，学生通过筛选后的规划、工具和反思轨迹学习单智能体决策。论文报告学生超过教师并降低开销，但其延迟仍以秒计，不能把“效率提升”写成已满足实时推荐要求。

[论文](https://arxiv.org/abs/2602.09829) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#star)

<a id="paper-rdrec"></a>
### RDRec: Rationale Distillation for LLM-based Recommendation

**2024-05 · arXiv** · `Top-N推荐` `序列推荐` `理由蒸馏` `画像`

将大模型从评论提炼的理由蒸馏给紧凑推荐模型，增强用户与物品画像；属于理由监督，不直接等同于预测时输出多步 CoT。作者仓库提示评论数据可能存在信息泄漏，阅读结果时需核对数据使用方式。

[论文](https://arxiv.org/abs/2405.10587) · [官方代码与作者说明](https://github.com/WangXFng/RDRec)

<a id="paper-slim"></a>
### SLIM: Can Small Language Models be Good Reasoners for Sequential Recommendation?

**2024-03 · arXiv** · `序列推荐` `CoT` `蒸馏` `推理增强表示`

把教师模型的逐步推理蒸馏给较小学生，再将学生生成的理由编码为特征参与推荐，体现推理增强表示的路线。

[论文](https://arxiv.org/abs/2403.04260) · 官方代码：未核实

<a id="agents"></a>
## 交互与智能体推荐

<a id="paper-re2a"></a>
### Re2A: Situated Conversational Recommendation via Rubric-based Preference Reasoning and Alignment

**2026-09 · arXiv** · `对话推荐` `多模态` `GRPO` `偏好对齐`

根据对话和共享视觉场景推断结构化偏好状态，用动态 rubric 奖励训练推理，再通过偏好条件 DPO 对齐回复与场景。模型裁判评分针对整条 thought/state，不等同逐推理步可验证奖励。

[论文](https://arxiv.org/abs/2609.18249) · 官方代码：未核实

<a id="paper-atomrec"></a>
### AtomRec: Evolving Atomic Memory for Agentic Recommendation

**2026-09 · arXiv** · `候选排序` `记忆` `证据路径` `多跳检索`

将用户与物品历史组织成可更新的原子记忆，推断语义关系并检索多跳证据路径，再综合证据排序候选；记忆构造、更新和在线证据合成均需计入成本。

[论文](https://arxiv.org/abs/2609.04882) · 官方代码：未核实

<a id="paper-reasonrec"></a>
### ReasonRec: A Reasoning-Augmented Multimodal Agent for Unified Recommendation

**2026-06 · arXiv** · `多模态` `CoT` `课程学习` `自适应计算`

将显式推理、逐步增加证据难度的课程学习和不确定性引导的任务委派结合，在统一推荐中分配模型计算。

[论文](https://arxiv.org/abs/2606.28357) · 官方代码：未核实

<a id="paper-next"></a>
### NEXT: Reasoning-Driven Video Recommendation via a Vision-Language Model

**2026-06 · arXiv** · `视频推荐` `意图推理` `VLM` `离线挖掘` `线上A/B`

用“视频 → 下一兴趣意图 → 后续视频”的路径生成和验证推荐关系，把推理得到的关系作为工业系统的额外召回通道。VLM 主要在离线或近线运行；论文报告的线上收益属于整条召回路径，不宜直接归因于某一个推理训练阶段。

[论文](https://arxiv.org/abs/2607.24789) · 官方代码：未核实

<a id="paper-twistar"></a>
### TwiSTAR: Think Fast, Think Slow, Then Act, Generative Recommendation with Adaptive Reasoning

**2026-05 · arXiv** · `工具选择`

训练规划器在快速 SID 检索、候选重排与慢速显式推理之间选择，利用协同关系转写的理由训练慢模型，并计入不同工具的调用成本。

[论文](https://arxiv.org/abs/2605.11553) · 官方代码：未核实

<a id="paper-intent-sid"></a>
### Intent-Driven Semantic ID Generation for Grounded Conversational News Recommendation

**2026-05 · arXiv** · `对话推荐` `CoT蒸馏` `语义ID`

用意图分析与教师思维链训练模型生成 SID 前缀，再与当前新闻池匹配；结合画像和行为证据处理冷启动，推荐项由实时语料库落地。

[论文](https://arxiv.org/abs/2605.07613) · 官方代码：未核实

<a id="paper-harpo"></a>
### HARPO: Hierarchical Agentic Reasoning for User-Aligned Conversational Recommendation

**2026-04 · arXiv** · `会话推荐` `树搜索` `多维奖励` `偏好优化`

结合质量价值网络引导的推理树搜索、相关性与多样性等分层偏好目标，以及抽象工具操作和多智能体精炼。其 MUSE 实验将图像转为文字描述，应标为文本推理迁移，不能据此认定为原生视觉推理。

[论文](https://arxiv.org/abs/2604.10048) · [官方代码](https://github.com/harpo-bench/harpo-crs) · [项目页](https://harpo-bench.github.io/) · [证据卡片](docs/frontier-reading.md#harpo)

<a id="paper-agenticrec"></a>
### AgenticRec: A Recommendation-Oriented Agentic Framework with Progressive Tool-Integrated Reasoning Optimization

**2026-03 · arXiv** · `工具推理` `GRPO` `困难负样本` `候选排序`

让用户画像、物品信息、行为统计和协同检索参与 Think–Act–Observation 决策循环；先以推荐反馈优化完整轨迹，再从排序错误挖掘难例进行双向偏好推理。实验采用 20 候选排序，不能直接推及全库召回。

[论文](https://arxiv.org/abs/2603.21613) · 作者匿名代码入口当前返回 403，内容未核实（见 [来源记录](docs/sources.md#unavailable-resources)）

<a id="paper-enf"></a>
### ENF: When Top-ranked Recommendations Fail: Modeling Multi-Granular Negative Feedback for Explainable and Robust Video Recommendation

**2025-11 · arXiv** · `视频推荐` `负反馈` `智能体` `RL`

结合用户画像、视频理解与综合推理三个智能体，预测负反馈并解释原因，使用渐进S-GRPO训练；推理同时参与用户参与度预测，不只是结果后的解释。属于显式多模态推理近邻，不是连续潜空间推理。

[论文](https://arxiv.org/abs/2511.18700) · 官方代码：未核实

<a id="paper-agentdr"></a>
### AgentDR: Dynamic Recommendation with Implicit Item-Item Relations via LLM-based Agents

**2025-10 · arXiv** · `动态推荐` `关系推理` `工具选择` `重排`

推断用户历史中的替代与互补关系，并选择、整合传统推荐器的输出，让关系推理参与最终排序。

[论文](https://arxiv.org/abs/2510.05598) · [阅读卡片](docs/reading-notes.md#agentdr) · 官方代码：未核实

<a id="benchmarks"></a>
## 评测、基准与有效性证据

包含 6 项评测资源与 7 篇有效性/协议研究。任务与指标不能直接合成统一排名，详见 [基准选型](docs/benchmarks.md)。

<a id="paper-transparent-upr"></a>
### Reproducing Transparent and Scrutable Recommendations: Exploring Open-Weight Models via Natural-Language User Profiles

**2026-09 · arXiv** · `评测研究` `画像干预` `偏好证据` `协议分析`

作者复现自然语言画像推荐，并以反事实画像和激活干预检查偏好证据是否影响排序；所测评分回归模型的表示和评分偏置会变，但未检测到显著类型选择性排序变化。结论受训练目标与候选协议限制，不能外推为 CoT 无效。

[论文](https://arxiv.org/abs/2609.19831) · [官方代码](https://github.com/nmamie/transparent_user_profiles)

<a id="paper-rpcbench"></a>
### RPCBench: A Benchmark for Proactive Premise Critique in LLM-based Recommendation

**2026-09 · arXiv** · `基准` `请求诊断` `证据忠实性` `过度推理`

评测模型能否主动识别、定位和处理推荐请求中的错误前提，并分析推理长度与诊断质量的关系。

[论文](https://arxiv.org/abs/2609.00918) · [官方代码](https://github.com/ZhongruChen/RPCBench)

<a id="paper-sidscope"></a>
### SIDScope：SIDScope: A Diagnostic Resource for Semantic-ID Interfaces in Generative Recommendation

**2026-08 · arXiv** · `评测研究` `SID` `可达性`

诊断物品到 SID 的映射结构、前缀候选暴露、路径到物品的解析及更新后的模型交接。它评估接口风险，不直接证明模型执行了潜在推理。

[论文](https://arxiv.org/abs/2608.18779) · 官方代码：未核实

<a id="paper-crs-protocol"></a>
### Retrieval, Scoring, and Decoding Shape Performance and Stability in LLM-based Conversational Recommendation

**2026-08 · arXiv** · `评测分析` `候选控制` `重排` `解码稳定性`

在 ReDial 上统一候选后比较 LLM 与传统重排器，分析候选生成、池大小、计分规则及温度如何改变结论。适合作为推理推荐的评测方法论：它不提出新的推理模型，也不单独证明 CoT 的有效或无效。

[论文](https://arxiv.org/abs/2609.00086) · [官方代码与输出](https://github.com/infobip/crs-performance) · [证据卡片](docs/frontier-reading.md#crs-protocol)

<a id="paper-lime-rec"></a>
### LIME-Rec: Auditing Semantic Gains in Sequential Recommendation: A Lightweight Recovery Test

**2026-08 · arXiv** · `评测分析`

用序列模型、物品共现与冻结文本表示的可检查分数融合，检验重型语义方法的收益能否由轻量模型获得；用物品—文本错配对照检查语义来源。

[论文](https://arxiv.org/abs/2608.01260) · [官方代码](https://github.com/Double-wk/LIME-Rec)

<a id="paper-disconnect"></a>
### The Disconnect Between Better Descriptive Reasoning Trace Quality and Recommendation Effectiveness

**2026-08 · arXiv** · `有效性研究` `控制实验` `CoT` `语义ID`

以物品表示（SID/Title）和显式推理（有/无）构成主控制实验，发现描述性轨迹质量提高不保证离线推荐效果提高。结论限于所测基座、三个 Amazon 领域及训练协议，不能外推为所有推理无效。

[论文](https://arxiv.org/abs/2608.23154) · 官方代码：未核实 · [证据卡片](docs/frontier-reading.md#disconnect)

<a id="paper-cold-sid"></a>
### Temporal Cold SID：Can Generative Recommendation Reach Cold Items? A Temporal Perspective on Semantic-ID Generation

**2026-07 · arXiv** · `评测研究` `SID` `冷启动`

使用绝对时间划分与前缀探查，区分已有 token 的重组和包含未见 token 的新物品生成；检查冷物品在编码与解码空间中是否可达。

[论文](https://arxiv.org/abs/2607.21101) · 官方代码：未核实

<a id="paper-tau-rec"></a>
### τ-Rec: A Verifiable Benchmark for Agentic Recommender Systems

**2026-06 · arXiv** · `基准` `对话推荐` `可验证奖励` `可靠性`

通过结构化目录条件验证推荐，并控制多轮对话中的约束揭示方式，考察智能体的约束满足和连续成功可靠性。其 `pass^k` 与“多次采样至少成功一次”的 `pass@k` 口径不同。

[论文](https://arxiv.org/abs/2606.10156) · [官方代码与数据入口](https://github.com/nbharaths/tau-rec)

<a id="paper-faithful-sid"></a>
### Faithful SID Evaluation：Faithful Evaluation of Semantic-ID Tokenizers for Generative Recommendation

**2026-05 · arXiv** · `评测研究` `SID` `碰撞`

区分命中 SID 与命中具体物品，分析编码碰撞引起的计分偏差，并提供物品级修正和消除碰撞的后处理。当前标题与初版不同，合并为一条。

[论文](https://arxiv.org/abs/2605.25330) · 官方代码：未核实

<a id="paper-conv-finre"></a>
### Conv-FinRe: A Conversational and Longitudinal Benchmark for Utility-Grounded Financial Recommendation

**2026-02 · arXiv** · `基准` `长期交互` `偏好推断` `多视角决策`

将实际选择、拟合效用、市场动量和风险偏好设为不同参照，检验对话推荐是否只是在模仿行为。真实行情及人类决策轨迹用于构造受控对话；效用参照来自模型假设，不能当作客观、唯一的用户最优决策。

[论文](https://arxiv.org/abs/2602.16990) · [官方代码](https://github.com/The-FinAI/Conv-FinRe) · [官方数据集合](https://huggingface.co/collections/TheFinAI/conv-finre)

<a id="paper-openonerec"></a>
### OpenOneRec Technical Report / RecIF-Bench

**2025-12 · arXiv** · `基准` `开放模型` `指令遵循` `多任务`

发布跨短视频、广告与商品的八任务评测、训练数据与推荐基础模型。收录价值在开放研究底座；其“推理”任务主要是推荐解释，因此八任务总分不等价于推理轨迹的因果忠实性。

[论文](https://arxiv.org/abs/2512.24762) · [官方代码、评测与资源入口](https://github.com/Kuaishou-OneRec/OpenOneRec)

<a id="paper-musicrs"></a>
### MusiCRS: Benchmarking Audio-Centric Conversational Recommendation

**2025-09 · arXiv** · `基准` `音频依据` `会话推荐` `模态消融`

把真实音乐讨论与音频关联，对比音频、文本及二者结合的推荐能力。它补足“偏好推理是否使用了声音证据”的评测入口，但本身不是 CoT 忠实性或强化学习基准。

[论文](https://arxiv.org/abs/2509.19469) · [官方代码](https://github.com/rohan2810/MusiCRS) · [官方数据](https://huggingface.co/datasets/rohan2810/MusiCRS)

<a id="paper-agentrecbench"></a>
### AgentRecBench: Benchmarking LLM Agent-based Personalized Recommender Systems

**2025-05 · arXiv** · `基准` `工具环境` `冷启动` `兴趣变化`

提供可查询的用户、评论与物品环境，评估普通推荐、用户或物品冷启动以及兴趣变化。虽然名为交互模拟环境，主要结果仍按历史真实物品的 20 候选命中率评测，不能解释为真实用户会话满意度。

[论文](https://arxiv.org/abs/2505.19623) · [官方数据](https://huggingface.co/datasets/SGJQovo/AgentRecBench) · [作者挑战与环境入口](https://tsinghua-fib-lab.github.io/AgentSocietyChallenge/pages/overview.html)

<a id="surveys"></a>
## 综述与研究路线

<a id="paper-agentic-roadmap"></a>
### Autonomous Information Seeking: A Roadmap for Agentic Recommender Systems

**2026-07 · arXiv** · `综述` `智能体角色` `轨迹评测`

从智能体辅助推荐、作为推荐器、作为用户模拟器等角色梳理自主信息获取，讨论轨迹评测和模拟器校准。作为领域导航，单列于新方法和基准之外。

[论文](https://arxiv.org/abs/2607.04433)

<a id="background"></a>
## 相关背景

以下工作帮助理解物品生成与推荐目标对齐，单独计为背景，不自动归入核心推理方法。

<a id="paper-hcg-rec"></a>
### HCGRec：Learning from Unreachable Rewards: Hint-Conditioned Reinforcement Learning for Generative Recommendation

**2026-08 · arXiv** · `背景` `生成式推荐` `RL` `前缀可达性`

在训练时对难例提供最短目标前缀提示，分别对提示 token 和采样后缀分配学习信号。属于 SID 奖励学习背景，目标提示不能用于部署评测。

[论文](https://arxiv.org/abs/2608.11980) · 官方代码：未核实

<a id="paper-latte"></a>
### Latte: Expressiveness Limits of Autoregressive Semantic ID Generation in Generative Recommendation

**2026-05 · arXiv** · `背景` `语义ID` `解码结构`

分析 SID 解码树与物品概率耦合，并以前置离散 latent token 条件化多棵树；另探索 token 与 SID 排列绑定。这里的 latent token 是离散路径变量，不是连续多步推理。

[论文](https://arxiv.org/abs/2605.06331) · [官方代码](https://github.com/hyp1231/Latte)

<a id="paper-mdgr"></a>
### MDGR: Masked Diffusion Generative Recommendation

**2026-01 · arXiv** · `背景` `语义ID` `掩码扩散` `并行解码`

结合并行码本、训练期掩码调度和两阶段并行解码，逐步补全物品编码。用于区分 SID 去噪与连续潜在推理的贡献，不因存在多步生成就视为推理方法。

[论文](https://arxiv.org/abs/2601.19501) · 官方代码：未核实

<a id="paper-tca4rec"></a>
### TCA4Rec: Token-level Collaborative Alignment for LLM-based Generative Recommendation

**2026-01 · arXiv** · `背景` `协同对齐` `软标签`

将协同过滤的物品分数转为生成 token 的软监督分布；是判断新增中间监督是否超出已有物品到 token 对齐的重要对照。原文任务包含物品标题生成，不将其限定为 SID 方法。

[论文](https://arxiv.org/abs/2601.18457) · [官方代码](https://github.com/critical88/TCA4Rec)

<a id="paper-maskgr"></a>
### MADRec / MaskGR: Masked Diffusion for Generative Recommendation

**2025-11 · arXiv** · `背景` `语义ID` `掩码扩散`

以随机掩码训练建模 SID 序列，支持双向条件和多位置并行补全，是比较联合编码推断的必要背景。v1 方法名为 MADRec，作者仓库当前使用 MaskGR 名称，合并维护为同一条。

[论文](https://arxiv.org/abs/2511.23021) · [官方代码](https://github.com/snap-research/MaskGR)

<a id="paper-onerec"></a>
### OneRec Technical Report

**2025-06 · arXiv** · `背景` `端到端生成式推荐` `RL`

介绍端到端生成式推荐的规模扩展、强化学习与工业实践，可作为理解 OneRec-Think 和 OneReason 的前置材料。

[论文](https://arxiv.org/abs/2506.13695) · 官方代码：未核实

<a id="paper-rec-r1"></a>
### Rec-R1: Bridging Generative Large Language Models and User-Centric Recommendation Systems via Reinforcement Learning

**2025-03 · arXiv** · `背景` `RL` `黑箱推荐反馈` `查询改写`

用固定推荐系统的反馈训练 LLM 生成查询改写、用户描述等输入，作为语言模型与推荐目标对齐的背景；不以显式推荐推理链为必要条件。

[论文](https://arxiv.org/abs/2503.24289) · [官方代码](https://github.com/linjc16/Rec-R1)

<a id="paper-setrec"></a>
### SETRec：Order-agnostic Identifier for Large Language Model-based Generative Recommendation

**2025-02 · arXiv** · `背景` `生成式推荐` `无序编码`

以无序 token 集合表达物品并并行生成，减弱固定序列依赖；是比较 SID 顺序与潜在推理时的重要编码对照。

[论文](https://arxiv.org/abs/2502.10833) · 官方代码：未核实

<a id="paper-tiger"></a>
### TIGER: Recommender Systems with Generative Retrieval

**2023-05 · arXiv** · `背景` `生成式检索` `语义ID`

将物品表示为语义 ID，通过自回归生成完成推荐，是理解物品编码与生成式检索的基础入口。

[论文](https://arxiv.org/abs/2305.05065) · 官方代码：未核实

## 下一步研究

从 [前沿地图](docs/frontier-map.md) 选择问题，再用 [方法对照](docs/method-matrix.md) 找控制组、[基准选型](docs/benchmarks.md) 选任务，按 [评测模板](docs/evaluation.md) 记录预算和证据。

## 维护与贡献

推荐论文可使用 Issue 模板，纠错和补充资源欢迎直接提交 PR。收录规则、条目模板及核实要求见 [贡献指南](CONTRIBUTING.md)。

本仓库用 Markdown 直接维护，链接检查随文档变更运行。分类与内容摘要需要人工核实；核实记录见 [来源索引](docs/sources.md)。

## 许可

本仓库原创整理文字采用 [CC BY 4.0](LICENSE)。外链论文、代码、模型和数据遵循各自许可。
