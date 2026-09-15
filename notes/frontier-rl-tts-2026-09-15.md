# RL、过程监督与自适应推理：2026-09-15 补充核实

本轮补充 9 篇 README 尚未收录的方法。截止日为 2026-09-15；日期采用 arXiv 首次提交日期，版本另列。资料层级为作者论文与作者链接的实现；未运行或复现实验。虽优先搜索 2026 年 7–9 月，新近 CoT/蒸馏、智能体和评测工作由另外两组处理，本组保留范围匹配的 2025 年关键遗漏和 2026 年方法，不以月份或数量代替相关性。

## 可直接用于 README 的条目

### ReRec: Reasoning-Augmented LLM-based Recommendation Assistant via Reinforcement Fine-tuning

**2026-04 · arXiv** · `推荐助手` `RFT` `奖励塑形` `推理步骤信用分配`

将排名、查询匹配和偏好匹配结合为奖励，按推理片段估计优势，并动态安排训练难度，使复杂推荐请求的多步分析与推荐目标对齐。

[论文](https://arxiv.org/abs/2604.07851) · [官方代码](https://github.com/jiani-huang/ReRec)

### SIDReasoner: Reasoning over Semantic IDs Enhances Generative Recommendation

**2026-03 · arXiv** · `序列推荐` `语义ID` `CoT` `GRPO`

增强语义 ID 与语言的多任务对齐，再通过推理激活和基于预测结果的 GRPO 优化推荐推理；奖励依据 SID 正确前缀与物品有效性，不能直接视为自然语言推理步骤正确性评分。

[论文](https://arxiv.org/abs/2603.23183) · [官方代码](https://github.com/HappyPointer/SIDReasoner)

### ManCAR: Manifold-Constrained Latent Reasoning with Adaptive Test-Time Computation for Sequential Recommendation

**2026-02 · arXiv** · `序列推荐` `潜在推理` `协同图约束` `自适应停止`

用协同交互图构造意图先验并约束潜在推理轨迹，在相邻步骤的预测分布收敛后停止，控制漂移和过度计算。

[论文](https://arxiv.org/abs/2602.20093) · [官方代码](https://github.com/FuCongResearchSquad/ManCAR)

### R2Rank: Reasoning to Rank: An End-to-End Solution for Exploiting Large Language Models for Recommendation

**2026-02 · arXiv** · `排名` `CoT` `PPO` `列表效用`

对每个用户—物品对单独推理与评分，再用 Plackett–Luce 排列代理将列表级推荐效用传回语言模型和评分头。

[论文](https://arxiv.org/abs/2602.12530) · 官方代码：未核实

### EGLR: Reasoning While Recommending: Entropy-Guided Latent Reasoning in Generative Re-ranking Models

**2026-01 · arXiv** · `生成式重排` `潜在推理` `熵门控` `自适应预算` `GRPO`

在列表逐项生成过程中，根据当前决策熵插入数量可变的潜在推理 token，并用不同温度调节推理探索和物品选择。

[论文](https://arxiv.org/abs/2601.13533) · 官方代码：未核实

### DTRec: Learning Dynamic Reasoning Trajectories for Sequential Recommendation

**2025-12 · arXiv** · `序列推荐` `层级过程监督` `潜在推理` `自适应停止`

以逐渐细化的物品聚类原型监督中间状态，并综合预测熵、相邻预测一致性和隐状态变化学习何时停止推理。

[论文](https://arxiv.org/abs/2512.14036) · 官方代码：未核实

### GREAM: Generative Reasoning Recommendation via LLMs

**2025-10 · arXiv** · `语义ID` `CoT` `课程学习` `SRPO`

通过协同语义对齐、合成思维链课程训练和稀疏奖励优化，支持直接物品生成与先推理再推荐两种模式；两种模式的评测指标需分别阅读。

[论文](https://arxiv.org/abs/2510.20815) · [官方代码](https://github.com/Indolent-Kawhi/GRRM)

### RecLLM-R1: A Two-Stage Training Paradigm with Reinforcement Learning and Chain-of-Thought v1

**2025-06 · arXiv** · `推荐列表` `CoT` `SFT` `GRPO` `多目标奖励`

先用用户历史与物品文本进行推荐 SFT，再以 GRPO 和多步思维链联合考虑准确性、多样性及业务目标。

[论文](https://arxiv.org/abs/2506.19235) · 官方代码：未核实

### R²ec: Towards Large Recommender Models with Reasoning

**2025-05 · arXiv** · `下一物品预测` `CoT` `双头模型` `RecPO`

在同一模型中分别生成推理链与预测物品，以融合奖励联合优化两者，减少独立推理模型与推荐器串联的开销。

[论文](https://arxiv.org/abs/2505.16994) · [官方代码与模型入口](https://github.com/YRYangang/RRec)

## 证据矩阵

下表的“局部”表示已阅读具体方法或实验章节，并非完整审稿。未列计算数字不等于论文没有报告。

| 方法 | 任务 | 推理表示 | 训练信号 | 推理计算方式 | 已核实证据 | 代码状态 |
| --- | --- | --- | --- | --- | --- | --- |
| ReRec | 复杂查询推荐助手 | 文本推理片段 | 排名＋查询/偏好对齐奖励；片段优势；训练课程 | 多步文本分析 | 摘要；方法结构 | 作者摘要直链，仓库可读 |
| SIDReasoner | 下一物品预测 | 文本推理＋SID | 多任务对齐、轻量激活、结果驱动 GRPO；前缀/格式奖励 | 推理后生成 SID | 局部 §3.3；源码首页明确三阶段 | 作者全文直链，仓库可读 |
| ManCAR | 序列推荐 | 潜在状态与物品分布 | 目标预测＋图先验 KL 约束 | 分布收敛提前停止 | 局部 §2.6、§3.3、§3.6；不是等预算对比 | 作者摘要直链，仓库可读 |
| R2Rank | 候选集排名 | 每候选文本推理＋评分头 | 自检 SFT；列表 NDCG；PPO/REINFORCE | 每候选独立推理后排序 | 局部 §3.3、§4.1、§4.3；固定 20 候选 | 未核实 |
| EGLR | 生成式重排 | 候选加权聚合的潜在 token | 预训练 evaluator 评分＋GRPO | 熵门控、每物品推理上限；多列表选择 | 局部 Algorithm 1、§5.6–5.7；收益递减 | 未核实 |
| DTRec | 序列推荐 | 潜在状态 | 原型过程监督＋软停止训练 | 三信号 MLP 停止概率，阈值提前退出 | 局部 §3.1–3.2；未精读预算实验 | 未核实 |
| GREAM | 生成式推荐 | 文本 CoT＋离散物品索引 | 合成轨迹 SFT；前缀奖励＋成功奖励 SRPO | direct/reason 双模式 | 局部 §5、§6.3；不同模式不同指标 | 作者全文直链，仓库可读 |
| RecLLM-R1 | 推荐列表 | 文本 CoT＋物品文本 | SFT＋GRPO 多目标奖励 | 多步文本决策 | 一手摘要；未核实等预算效果 | 未核实 |
| R²ec | 下一物品推荐 | 文本链＋独立推荐头 | RecPO 融合奖励 | 链生成后推荐头物品预测 | 一手摘要；未精读预算对照 | 作者摘要直链，仓库可读 |

## 局部证据卡

### ManCAR：训练步数和推理步数应分别计算

图先验约束中间物品分布，并以相邻步骤 KL 小于阈值提前停止。Table 3 中 CDs 最佳设置训练 5 步、平均推理 1.84 步，Arts 则均为 1 步。该表比较各方法最佳设置，**并未固定训练或总计算预算**，不能把步数差直接当作公平加速比。§3.6 仅显示相邻预测逐渐稳定，稳定不等于预测正确；还需结合排名指标与去图约束消融判断。归为自适应潜在推理，不是文字 CoT。[v1 §2.6](https://arxiv.org/html/2602.20093v1#S2.SS6) · [v1 §3.3](https://arxiv.org/html/2602.20093v1#S3.SS3) · [v1 §3.6](https://arxiv.org/html/2602.20093v1#S3.SS6)

### EGLR：额外深度的收益递减，候选选择指标不能混用

以熵门控决定是否插入潜在 token，`Smax` 限制每物品推理步数。KuaiRand 的 Table 4 中上限 0/1/3 对应 NDCG@10 为 0.7443/0.7526/0.7541，增益递减；单张 3090 所报时延为 38.14/54.89/86.18 秒，但表未明确按单请求或整个评测统计，不能转成单请求时延。Table 5 增加生成列表数主要提高 evaluator 分数，MAP 未逐项单调上升；该文“Pass@K”指多列表生成选择设置。[v1 Algorithm 1](https://arxiv.org/html/2601.13533v1#S4) · [v1 §5.6–5.7](https://arxiv.org/html/2601.13533v1#S5.SS6)

### R2Rank：有训练期 CoT 消融，但不是等 token 推理实验

模型对候选逐个推理，用列表 NDCG 奖励联合优化主干和评分头。§4.3 在同一 Qwen2.5-3B、每例 1 正例＋19 负例协议下，改变 RL 训练提示以允许或禁止 CoT；Table 5 的 Video Games NDCG@10 为 0.596 对 0.458。它支持训练期间输出推理的作用，但不是冻结同一模型、匹配 token 或时延的测试时比较，也不能外推到全目录检索。SFT 冷启动与联合训练另有消融。[v1 §3.3](https://arxiv.org/html/2602.12530v1#S3.SS3) · [v1 §4.1](https://arxiv.org/html/2602.12530v1#S4.SS1) · [v1 §4.3](https://arxiv.org/html/2602.12530v1#S4.SS3)

### GREAM：奖励优化对两种生成模式有取舍

前缀奖励缓解稀疏反馈，成功奖励补偿精确命中的训练信号。Instruments 的 Table 3 中课程激活后 direct 平均指标为 0.0949；加 GRPO 后降至 0.0921，而 reason 指标从 0.0656 升至 0.0741。后续完整奖励组合的 reason 为 0.0753。direct 平均混合 Recall/NDCG，reason 平均则是 Pass@1/5/10，不能横向相减。§6.4 扩展的是合成轨迹训练数据与训练 FLOPs，不能标为测试时 scaling 实验。[v1 §5](https://arxiv.org/html/2510.20815v1#S5) · [v1 §6.3–6.4](https://arxiv.org/html/2510.20815v1#S6.SS3)

## 一手来源与版本台账

| 方法 | 首次日期（UTC） | 读取版本 | 一手证据与资源归属 |
| --- | --- | --- | --- |
| ReRec | 2026-04-09 | v1 | [摘要/历史](https://arxiv.org/abs/2604.07851)直接提供 [jiani-huang/ReRec](https://github.com/jiani-huang/ReRec)，页面可读 |
| SIDReasoner | 2026-03-24 | v2（2026-06-09） | [摘要/历史](https://arxiv.org/abs/2603.23183)；[全文](https://arxiv.org/html/2603.23183v2)直链 [HappyPointer/SIDReasoner](https://github.com/HappyPointer/SIDReasoner)，页面可读；另有作者提供的 [Zenodo DOI](https://doi.org/10.5281/zenodo.20508816)，未核归档内容 |
| ManCAR | 2026-02-23 | v1 | [摘要/历史](https://arxiv.org/abs/2602.20093)直链 [FuCongResearchSquad/ManCAR](https://github.com/FuCongResearchSquad/ManCAR)，页面可读 |
| R2Rank | 2026-02-13 | v1 | [摘要/历史](https://arxiv.org/abs/2602.12530)及[全文](https://arxiv.org/html/2602.12530v1)；未定位作者代码链接 |
| EGLR | 2026-01-20 | v1 | [摘要/历史](https://arxiv.org/abs/2601.13533)及[全文](https://arxiv.org/html/2601.13533v1)；未定位作者代码链接 |
| DTRec | 2025-12-16 | v1 | [摘要/历史](https://arxiv.org/abs/2512.14036)及[全文](https://arxiv.org/html/2512.14036v1)；未定位作者代码链接 |
| GREAM | 2025-10-23 | v1 | [摘要/历史](https://arxiv.org/abs/2510.20815)；[全文](https://arxiv.org/html/2510.20815v1)提供 [Indolent-Kawhi/GRRM](https://github.com/Indolent-Kawhi/GRRM)；首页已有 SRPO 训练和两类评测命令 |
| RecLLM-R1 | 2025-06-24 | v1 | [摘要/历史](https://arxiv.org/abs/2506.19235)的标题末尾确有 `v1`；[全文标题](https://arxiv.org/html/2506.19235v1)未带该后缀，README 可保留摘要页写法；未定位作者代码链接 |
| R²ec | 2025-05-22 | v3（2025-10-31） | [摘要/历史](https://arxiv.org/abs/2505.16994)直链 [YRYangang/RRec](https://github.com/YRYangang/RRec)，页面可读 |

### 维护时的关键边界

- **SIDReasoner：** 摘要概括两阶段，而方法及代码将推理激活另列一步；不要将“无需大量人工推理标注”改写成“完全不使用任何推理轨迹”。[方法 §3.3](https://arxiv.org/html/2603.23183v2#S3.SS3)
- **GREAM / SIDReasoner：** 对 SID 前缀给予部分奖励，仍然不等于逐句核验语言推理正确性。
- **ManCAR / DTRec：** 属于非文本的潜在状态计算，过程监督无需贴 RL 标签。
- **所有代码：** “官方”仅表示来源归属与页面可读，本轮没有测试安装、训练、数据完整性或报告复现。
- **未纳入主列表的检索线索：** [Learning User Interests via Reasoning and Distillation for Cross-Domain News Recommendation](https://arxiv.org/abs/2602.15005) 侧重兴趣查询生成与下游检索，未进一步核实推理链和预算对照；[Exploring Test-time Scaling via Prediction Merging on Large-Scale Recommendation](https://arxiv.org/abs/2512.07650) 主要是预测集成，尚不足以直接视为推荐推理核心。
