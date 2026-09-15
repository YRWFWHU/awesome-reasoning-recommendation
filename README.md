# Awesome Reasoning for Recommendation

**推理增强推荐：思维链、强化学习与推理时扩展。**

精选论文、官方实现与评测资源，围绕三个问题组织：**推理了什么？推理有效吗？成本是多少？**

[入门路线](#start-here) · [论文清单](#papers) · [阅读卡片](docs/reading-notes.md) · [评测指南](docs/evaluation.md) · [参与贡献](CONTRIBUTING.md)

**最近整理：2026-09-15** · 20 篇核心条目（含 2 项基准）· 3 篇背景 · 5 篇阅读卡片

## 收录范围

关注推理如何参与推荐决策，包括显式文本思维链、潜在状态迭代、结构化路径搜索、推理蒸馏、奖励学习，以及智能体的工具选择与交互规划。

- **核心方法**：推理用于偏好理解、物品选择、排序、重排或交互决策。
- **评测资源**：检验推荐推理、约束满足、证据使用及决策可靠性。
- **相关背景**：生成式检索、物品编码及推荐目标对齐，单列为阅读前置。

使用 LLM、强化学习或生成物品 ID，本身不足以说明具备推荐推理能力。仅在结果产生后补充解释的工作，需另行说明与决策的关系。这里的分类是仓库的编辑约定。

### 如何阅读条目

- 日期采用 **arXiv 首次提交月份**；`arXiv` 表示来源，不表示论文一定未经同行评审。首版不统一标注未经独立核实的会议录用信息。
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
| 如何控制推理成本 | [SLIM](#paper-slim) → [WhisperRec](#paper-whisperrec) → [AgentDR](#paper-agentdr) | 哪些计算可蒸馏、缓存或交给工具？ |
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

<a id="papers"></a>
## 论文清单

- [思维链与推理学习](#cot)
- [强化学习与奖励设计](#rl)
- [推理时扩展](#tts)
- [推理蒸馏与效率](#distillation)
- [交互与智能体推荐](#agents)
- [评测与基准](#benchmarks)
- [相关背景](#background)

<a id="cot"></a>
## 思维链与推理学习

<a id="paper-onereason"></a>
### OneReason Technical Report

**2026-06 · arXiv · 进行中的技术报告** · `CoT` `SFT` `RL` `物品语义对齐`

通过物品语义感知、三层推荐思维链和分阶段强化学习增强推荐推理；同时研究 thinking 与 non-thinking 的差异，适合追问推理收益究竟来自训练还是预测阶段。

[论文](https://arxiv.org/abs/2606.06260) · [阅读卡片](docs/reading-notes.md#onereason) · 官方代码：未核实

<a id="paper-onerec-think"></a>
### OneRec-Think: In-Text Reasoning for Generative Recommendation

**2025-10 · arXiv** · `序列推荐` `CoT` `GRPO` `物品语义对齐`

先对齐物品与文本语义，再学习推荐推理轨迹并用推荐奖励优化，使文本推理参与后续物品生成。

[论文](https://arxiv.org/abs/2510.11639) · [官方代码](https://github.com/wangshy31/OneRec-Think) · [阅读卡片](docs/reading-notes.md#onerec-think)

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

<a id="paper-gr2"></a>
### GR2: Generative Reasoning Re-ranker

**2026-02 · arXiv** · `重排` `CoT` `SFT` `DAPO` `奖励设计`

结合语义 ID 训练、教师推理轨迹和 DAPO 优化候选重排，并针对保留原候选顺序的奖励投机设计条件奖励。

[论文](https://arxiv.org/abs/2602.07774) · [阅读卡片](docs/reading-notes.md#gr2) · 官方代码：未核实

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

交叉阅读：[OneRec-Think](#paper-onerec-think)、[OneReason](#paper-onereason)、[R2Rec](#paper-r2rec) 也包含奖励学习。

<a id="tts"></a>
## 推理时扩展

本专题分别标注潜在状态迭代、候选验证和结构化路径搜索，避免将它们统一描述为文本思维链。

<a id="paper-promise"></a>
### PROMISE: Process Reward Models Unlock Test-Time Scaling Laws in Generative Recommendations

**2026-01 · arXiv** · `生成式推荐` `过程奖励` `束搜索` `结构化路径`

通过过程奖励评估层级语义 ID 的中间生成步骤，并引导测试时搜索。这里的推理对象是结构化生成路径，归入搜索与验证，不标为自然语言 CoT。

[论文](https://arxiv.org/abs/2601.04674) · 官方代码：未核实

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

交叉阅读：[ReasonRec](#paper-reasonrec) 研究自适应任务委派，属于计算分配，不等同于证明推理预算的 scaling law。

<a id="distillation"></a>
## 推理蒸馏与效率

<a id="paper-whisperrec"></a>
### WhisperRec: Latent Reasoning for Efficient Foundation Recommendation Models

**2026-07 · arXiv** · `CoT压缩` `潜在推理` `蒸馏`

将教师的多视角思维链压缩为可学习的潜在推理 token，结合对齐和课程式后训练，减少显式理由生成的开销。

[论文](https://arxiv.org/abs/2607.26621) · 官方代码：未核实

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

交叉阅读：[EXP3RT](#paper-exp3rt) 也使用推理数据蒸馏；[OneRec-Think 阅读卡片](docs/reading-notes.md#onerec-think) 介绍离线推理与在线生成的分工。

<a id="agents"></a>
## 交互与智能体推荐

<a id="paper-reasonrec"></a>
### ReasonRec: A Reasoning-Augmented Multimodal Agent for Unified Recommendation

**2026-06 · arXiv** · `多模态` `CoT` `课程学习` `自适应计算`

将显式推理、逐步增加证据难度的课程学习和不确定性引导的任务委派结合，在统一推荐中分配模型计算。

[论文](https://arxiv.org/abs/2606.28357) · 官方代码：未核实

<a id="paper-agentdr"></a>
### AgentDR: Dynamic Recommendation with Implicit Item-Item Relations via LLM-based Agents

**2025-10 · arXiv** · `动态推荐` `关系推理` `工具选择` `重排`

推断用户历史中的替代与互补关系，并选择、整合传统推荐器的输出，让关系推理参与最终排序。

[论文](https://arxiv.org/abs/2510.05598) · [阅读卡片](docs/reading-notes.md#agentdr) · 官方代码：未核实

<a id="benchmarks"></a>
## 评测与基准

<a id="paper-rpcbench"></a>
### RPCBench: A Benchmark for Proactive Premise Critique in LLM-based Recommendation

**2026-09 · arXiv** · `基准` `请求诊断` `证据忠实性` `过度推理`

评测模型能否主动识别、定位和处理推荐请求中的错误前提，并分析推理长度与诊断质量的关系。

[论文](https://arxiv.org/abs/2609.00918) · [官方代码](https://github.com/ZhongruChen/RPCBench)

<a id="paper-tau-rec"></a>
### τ-Rec: A Verifiable Benchmark for Agentic Recommender Systems

**2026-06 · arXiv** · `基准` `对话推荐` `可验证奖励` `可靠性`

通过结构化目录条件验证推荐，并控制多轮对话中的约束揭示方式，考察智能体的约束满足和连续成功可靠性。其 `pass^k` 与“多次采样至少成功一次”的 `pass@k` 口径不同。

[论文](https://arxiv.org/abs/2606.10156) · [官方代码与数据入口](https://github.com/nbharaths/tau-rec)

评测协议和复现状态的记录方式见 [评测指南](docs/evaluation.md)。

<a id="background"></a>
## 相关背景

以下工作帮助理解物品生成与推荐目标对齐，单独计为背景，不自动归入核心推理方法。

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

<a id="paper-tiger"></a>
### TIGER: Recommender Systems with Generative Retrieval

**2023-05 · arXiv** · `背景` `生成式检索` `语义ID`

将物品表示为语义 ID，通过自回归生成完成推荐，是理解物品编码与生成式检索的基础入口。

[论文](https://arxiv.org/abs/2305.05065) · 官方代码：未核实

## 值得继续研究的问题

- **推理增益来自哪里？** 额外监督、语义对齐、预测时推理和更多候选各贡献多少？
- **中间分析是否影响结果？** 替换或打乱推理后，最终选择如何变化？
- **奖励会鼓励什么捷径？** 格式、候选位置、热门偏置是否替代了偏好推理？
- **预算如何分配？** 哪些用户或请求值得使用更多推理，何时应停止？
- **真实交互能否验证？** 模拟用户、离线排序与实际使用反馈之间有哪些差异？

## 维护与贡献

推荐论文可使用 Issue 模板，纠错和补充资源欢迎直接提交 PR。收录规则、条目模板及核实要求见 [贡献指南](CONTRIBUTING.md)。

本仓库用 Markdown 直接维护，链接检查随文档变更运行。分类与内容摘要需要人工核实；核实记录见 [来源索引](docs/sources.md)。

## 许可

本仓库原创整理文字采用 [CC BY 4.0](LICENSE)。外链论文、代码、模型和数据遵循各自许可。
