# 推理增强推荐 Awesome 仓库：范围调研

调研日期：2026-09-15。按用户最新选择，聚焦思维链、强化学习和推理时扩展，建议名称为 `awesome-reasoning-recommendation`。

本笔记是用于确定收录边界的有限抽样：阅读了 6 篇论文的一手摘要页、2 个相关 Awesome 仓库原页。不是最新完整论文清单；未精读全文、复现实验或全面核查代码。下列年份采用 arXiv 首次提交年份，不能直接当作会议发表年份。

## 一、代表样本与边界

| 论文 | 摘要中可核实的内容 | 建议位置 |
| --- | --- | --- |
| [OneRec-Think: In-Text Reasoning for Generative Recommendation](https://arxiv.org/abs/2510.11639)（2025） | 通过物品与文本对齐、推理激活、推荐专用奖励，结合对话、推理和推荐。 | 核心：显式推理与奖励优化 |
| [GR2: Generative Reasoning Re-ranker](https://arxiv.org/abs/2602.07774)（2026） | 重排任务中使用教师生成推理轨迹、监督微调及 DAPO；报告保持原有物品顺序造成奖励投机的问题。 | 核心：推理重排、RL、奖励设计 |
| [OneReason Technical Report](https://arxiv.org/abs/2606.06260)（2026） | 作者称早期研究中 thinking 模式未优于 non-thinking；提出物品语义感知、三层 CoT 与 RL 训练方案。页面注明 Work in progress。 | 核心：推理有效性与评估 |
| [Test-Time Scaling Strategies for Generative Retrieval in Multimodal Conversational Recommendations](https://arxiv.org/abs/2508.18132)（2025） | 在多模态对话商品检索中，对生成式检索增加测试时重排以适应变化的用户意图。 | 核心：推理时计算扩展；场景标注为对话商品检索 |
| [Recommender Systems with Generative Retrieval（TIGER）](https://arxiv.org/abs/2305.05065)（2023） | 以 Semantic ID 表示物品，自回归生成下一物品标识。 | 背景：生成式检索和物品表征 |
| [OneRec Technical Report](https://arxiv.org/abs/2506.13695)（2025） | 端到端生成式推荐，讨论规模扩展、强化学习和工业部署。 | 背景：端到端生成式推荐；不能仅凭使用 RL 就归为显式推理 |

## 二、与现有仓库的关系

- [hyp1231/awesome-generative-recommendation](https://github.com/hyp1231/awesome-generative-recommendation) 的范围较广，原页包括 LLM 推荐对齐、生成式检索、物品索引及解释等方向。
- [jihoo-kim/Awesome-Generative-RecSys](https://github.com/jihoo-kim/Awesome-Generative-RecSys) 使用标题、发表信息、论文和代码的表格，覆盖扩散模型、GAN、VAE、生成式检索等多种生成方法。

**编辑建议（基于以上抽样的判断）：** 新仓库可围绕“推理如何参与推荐决策、带来什么增益、付出多少计算成本”组织资料，生成式推荐仅保留必要背景。这里不声称该定位没有其他竞争仓库。

## 三、建议收录规则

以下是建议的编辑规则，不是领域公认定义：

1. **核心收录：** 推理轨迹、规划、搜索、自我修正、推理蒸馏，或针对推荐推理的奖励学习与推理时计算扩展，实际参与推荐、排序、重排或对话推荐决策。
2. **RL 单独判定：** 记录它是在训练推理过程，还是仅优化物品生成、点击或长期收益；后者可进入背景，不自动归为推理增强。
3. **解释单独判定：** 记录解释是否在决策前参与计算，还是在结果产生后生成；证据不足时标注“待核实”。
4. **TTS 单独判定：** 记录增加的是推理长度、候选数、搜索、验证器还是重排计算，并记录可得的延迟或计算预算。
5. **背景收录：** TIGER、OneRec 等用于理解表征和生成范式；普通 LLM 特征提取、泛化的生成式数据增强不进入主列表。

## 四、建议目录与特色字段

目录建议：入门路线 → 思维链与推理数据 → 强化学习与奖励 → 推理时扩展与搜索 → 推理蒸馏与效率 → 评估与基准 → 生成式推荐背景。

每篇先提供标题、年份、任务、方法标签、一句话贡献、论文和代码链接。精选论文再提供详细卡片：

- 推理形式，以及推理在训练期和推理期的位置。
- 奖励来源和目标；是否有奖励投机检查。
- 与不推理模型的对照；是否控制模型规模、数据、候选集和计算预算。
- 质量指标与延迟、生成 token 数、采样次数等成本指标。
- 代码、模型、数据的发布情况，分别标注“官方”“第三方”“未核实”。

这些字段的动机来自样本中可见的问题：OneReason 关注 thinking 的实际增益，GR2 关注奖励投机，多模态对话 TTS 关注测试时重排。只读摘要尚不足以给这些论文填写全部评估字段；此处提出的是后续精读框架。
