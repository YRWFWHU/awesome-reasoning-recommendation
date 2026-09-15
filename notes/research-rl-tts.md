# 强化学习、推理时计算与智能体推荐：首批核实记录

核实日期：2026-09-15。以下日期均为 arXiv 首次提交日期（UTC），不是会议日期；归类与收录理由是本仓库编辑判断。每篇先核对 arXiv 摘要与提交记录，再在必要时核对全文。未运行论文代码、未复现实验，实验结果均为作者报告。

核实层级：**摘要核实**＝已阅读一手摘要及版本记录；**全文局部核实**＝另读方法、消融或成本相关章节；**官方链接核实**＝作者论文直接链接仓库，且仓库页面可读。仅从题目猜测代码地址不计核实。

## 可直接整合到 README 的核心条目

| 首次日期 | 论文 | 任务与标签 | 一句话贡献 | 官方代码 | 核实层级 |
| --- | --- | --- | --- | --- | --- |
| 2025-10-07 | **AgentDR: Dynamic Recommendation with Implicit Item-Item Relations via LLM-based Agents** · [论文](https://arxiv.org/abs/2510.05598) | 动态推荐、重排；`Agent` `工具选择` `关系推理` | 利用 LLM 推断用户历史中的替代与互补关系，并选择和整合传统推荐工具的排序结果。 | 未核实 | 全文局部核实 |
| 2025-10-27 | **MGFRec: Towards Reinforced Reasoning Recommendation with Multiple Groundings and Feedback** · [论文](https://arxiv.org/abs/2510.22888) | 物品推荐；`GRPO` `多轮推理` `物品对齐` `用户模拟` | 在推理期间多次对齐真实物品空间，并通过用户智能体反馈与 GRPO 训练修正推荐推理。 | 未核实 | 摘要核实；训练方法节核对 |
| 2026-01-08 | **PROMISE: Process Reward Models Unlock Test-Time Scaling Laws in Generative Recommendations** · [论文](https://arxiv.org/abs/2601.04674) | 生成式检索；`TTS` `PRM` `结构化路径搜索` | 在各层语义 ID 路径上训练过程奖励模型，并据其中间路径评分筛选束搜索候选，以扩展测试时搜索。 | 未核实 | 摘要核实；方法 §3.2–3.3 核实 |
| 2026-05-17 | **SAPO: Step-Aligned Policy Optimization for Reasoning-Based Generative Recommendation** · [论文](https://arxiv.org/abs/2605.17648) | 下一物品预测；`RLVR` `信用分配` `语义ID` | 将每个思考块与对应语义 ID token 组成推理步骤，按步骤计算组相对优势，改进稀疏结果奖励的信用分配。 | `https://github.com/zhengzaiyi/SAPO`；页面可用性未核实 | 摘要核实；全文官方链接已定位 |
| 2026-05-21 | **Reinforced Preference Optimization for Reasoning-Augmented Recommendations**（RPORec）· [论文](https://arxiv.org/abs/2605.21967) | 个性化物品检索；`CoT` `RL` `推荐头` | 用思维链辅助推荐头学习，再以推荐头提供的可验证奖励优化 LLM 推理，使推理与检索目标对齐。 | 未核实 | 摘要核实 |
| 2026-06-08 | **ReasonRec: A Reasoning-Augmented Multimodal Agent for Unified Recommendation** · [论文](https://arxiv.org/abs/2606.28357) | 多模态推荐；`Agent` `CoT` `自适应计算` | 结合显式推理、逐步增加证据难度的课程学习与不确定性引导的任务委派，兼顾推荐表现和推理效率。 | 未核实 | 摘要核实 |
| 2026-06-08 | **τ-Rec: A Verifiable Benchmark for Agentic Recommender Systems** · [论文](https://arxiv.org/abs/2606.10156) | 多轮对话推荐评测；`Benchmark` `可验证奖励` `可靠性` | 用结构化目录条件验证推荐结果，并控制对话中约束的揭示方式，评测推荐智能体的连续成功可靠性。 | [代码与数据](https://github.com/nbharaths/tau-rec) | 摘要核实；官方链接核实 |
| 2026-09-01 | **RPCBench: A Benchmark for Proactive Premise Critique in LLM-based Recommendation** · [论文](https://arxiv.org/abs/2609.00918) | 推荐请求诊断；`Benchmark` `证据忠实性` `过度推理` | 评测模型能否主动识别、定位和处理推荐请求的错误前提，并分析推理长度与诊断质量的关系。 | [代码](https://github.com/ZhongruChen/RPCBench) | 摘要核实；官方链接核实 |

## 每篇的收录理由与来源边界

### AgentDR

- **收录理由：** 推理直接参与推荐工具选择及候选重排，适合作为“智能体如何使用传统推荐器”的入口，而非仅生成事后解释。[摘要与版本记录](https://arxiv.org/abs/2510.05598)
- **正式记录：** 摘要页标注 WWW 2026 长文；此处根据作者维护的 arXiv 记录，尚未另核会议目录。
- **资源：** 全文中的 GitHub 链接未定位到该项目代码，因此保留“未核实”。不表示作者一定未开源。

### MGFRec

- **收录理由：** 推理过程中交替接触真实物品与用户反馈，直接回应纯语言空间推理偏离实际推荐目录的问题。[摘要](https://arxiv.org/abs/2510.22888)
- **训练证据：** 全文 §4.4 明确列出 RL-based Training、GRPO with Multiple Groundings and Feedback、Reward Modeling；用户智能体是方法中的模拟反馈来源，不能写成已验证的真实用户在线反馈。[全文](https://arxiv.org/html/2510.22888v2#S4.SS4)
- **正式记录：** 摘要页标注 Accepted at KDD 2026，未另核会议目录。

### SAPO

- **收录理由：** 优化对象包含显式 thinking block，不只是使用 RL 生成物品 ID；其亮点是推理步骤与输出层级对应的奖励分配。[摘要与版本记录](https://arxiv.org/abs/2605.17648)
- **版本：** 首次为 2026-05-17；本次读取的是 2026-08-15 修订的 v2，不应将修订日期当首次日期。
- **代码证据：** [全文摘要](https://arxiv.org/html/2605.17648v2)直接给出 `https://github.com/zhengzaiyi/SAPO`；本次浏览代码页发生 Internal Error，所以只确认作者链接，未确认仓库内容。

### RPORec

- **收录理由：** 显式连接思维链、推荐表示与 RL 奖励，适合比较“语言推理如何接入精确物品检索”。[摘要与版本记录](https://arxiv.org/abs/2605.21967)
- **证据边界：** 摘要报告公开数据及大规模在线部署结果；本次未核对具体实验协议或数字。全文未找到可直接归属的代码仓库。[全文](https://arxiv.org/html/2605.21967v1)

### ReasonRec

- **收录理由：** 推理链外还包含基于不确定性的委派机制，可填补自适应计算和多模态推荐交叉部分。[摘要与版本记录](https://arxiv.org/abs/2606.28357)
- **证据边界：** 摘要报告可将部分请求委派至高效子模型；应归为“自适应计算”，不能据此宣称已经验证增加推理预算的 scaling law。
- **日期注意：** 摘要页 Submission history 为 2026-06-08，虽然编号为 2606.28357；依一手历史记录填写日期，不从编号末位推断提交日。

### τ-Rec

- **收录理由：** 评测多轮澄清后的约束满足和重复执行可靠性，补充只报告一次离线排名指标的盲区。[摘要与版本记录](https://arxiv.org/abs/2606.10156)
- **资源归属：** 摘要中的代码链接指向 [nbharaths/tau-rec](https://github.com/nbharaths/tau-rec)，仓库首页标题与论文匹配，页面已读。
- **证据边界：** 此处的 `pass^k` 是可靠性口径，不要与“k 次采样中至少成功一次”的 `pass@k` 混用。摘要列出的模型家族数与具体名单不完全一致，README 不复述该计数。

### RPCBench

- **收录理由：** 把推荐推理评测扩展到检查请求前提、证据定位和处理策略，并提供推理更长并不单调更好的研究问题。[摘要与版本记录](https://arxiv.org/abs/2609.00918)
- **资源归属：** 摘要与 Comments 的代码链接均指向 [ZhongruChen/RPCBench](https://github.com/ZhongruChen/RPCBench)，仓库页面标注为该论文官方实现。
- **证据边界：** 摘要报告 5 个领域、10 类前提错误和 11 个 LLM；本次没有复核数据构造或长度实验全文，不能把相关性改写为因果结论。

## 第五篇深入阅读卡片候选：AgentDR

**推理了什么？** 根据近期交互推断替代品与互补品，并据候选结果和用户偏好选择推荐工具；这些信号用于候选重排。[§3.3–3.6](https://arxiv.org/html/2510.05598v3#S3.SS3)

**推理有效吗？** Table 5 比较同一聚合器加或不加 LLM 模块：例如 RC 在 Instacart 的 NDCG@10 从 0.0428 变为 0.0701。§4.6 的消融显示双重替代/互补重排优于单一方向；工具比较在 Instacart 有退化，不能写成所有模块始终有益。[§4.5–4.6](https://arxiv.org/html/2510.05598v3#S4.SS5)

**成本是多少？** 作者给出总调用数 `6n + 3nt`（n 为用户数，t 为优化轮数），并报告记忆更新完成后每用户生成最终列表少于 1 秒；实验使用 Phi-4、vLLM 和 8 张 32GB V100。该延迟不包含前置记忆优化，不能当成完整链路时延。[Appendix A.1–A.2](https://arxiv.org/html/2510.05598v3#A1.SS2)

**限制。** 消融支持模块的任务收益，尚不等于推理文本忠实性验证；作者指出替代/互补关系的适用性依赖领域。[§5](https://arxiv.org/html/2510.05598v3#S5)

## 相邻背景：Rec-R1

| 首次日期 | 论文 | 标签 | 条目 |
| --- | --- | --- | --- |
| 2025-03-31 | **Rec-R1: Bridging Generative Large Language Models and User-Centric Recommendation Systems via Reinforcement Learning** · [论文](https://arxiv.org/abs/2503.24289) · [官方代码](https://github.com/linjc16/Rec-R1) | `RL` `黑箱推荐反馈` `查询改写` `偏好摘要` | 用固定推荐系统的检索或排序反馈，训练 LLM 生成查询改写、用户描述等推荐输入，作为 RL 与推荐目标对齐的背景。 |

核实层级：摘要、全文局部、官方代码链接均已核实；全文 v4 摘要直接链接代码仓库，仓库页面可读。arXiv Comments 标注发表于 TMLR。[全文](https://arxiv.org/html/2503.24289v4)

**不建议作为核心推理卡片：** §1 与 §2 将优化对象定义为推荐器消费的文本，不以显式推理步骤为必要条件；“保留通用推理能力”的实验不能直接证明推荐决策推理链有效。[§1–2](https://arxiv.org/html/2503.24289v4#S2)

## 补核实：PROMISE 的结构化路径搜索

**收录判断：** 适合纳入推理时扩展。仓库允许潜在推理和搜索，因此不应将“存在显式文字 CoT”作为必要条件。准确标题与首次日期已由 [arXiv 摘要及提交记录](https://arxiv.org/abs/2601.04674)核实：**PROMISE: Process Reward Models Unlock Test-Time Scaling Laws in Generative Recommendations**，2026-01-08。

**机制：** PRM 输入用户、上下文及不同深度的 SID 前缀，输出该路径与用户的相关性分数；用真实物品前缀和采样负路径做 InfoNCE 训练。测试时先按生成概率选出较大的 `K+` 路径集合，再按 PRM 分数仅保留 `K′` 条路径继续解码；这是对中间状态的验证和搜索，而非仅对完整推荐结果评分。[方法 §3.2–3.3](https://arxiv.org/html/2601.04674v1#S3)

**边界与资源：** 标签使用“结构化路径搜索，非文本 CoT”。训练是下一 token 损失与对比损失联合优化，不能因名称含 reward 就归为 RL。官方代码未核实：摘要及方法全文未找到作者代码链接。论文标题中的 scaling laws 是作者主张，方法核实本身不等于全面验证该规律。[全文](https://arxiv.org/html/2601.04674v1)

## 其他范围说明

没有为满足数量而加入纯传统 RL 推荐综述、仅输出推荐理由的领域应用，或通用 LLM 推理方法论文。

## 后续链接核查

2026-09-15 的自动访问检查发现 R2Rec 作者匿名入口返回 401，SAPO 作者代码地址返回 404。原地址作为文字保留，不标为可用资源；详细记录见 [来源索引](../docs/sources.md#unavailable-resources)。
