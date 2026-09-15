# 思维链、推理学习与推理蒸馏：首批核实条目

核实日期：2026-09-15。本组共 8 篇，均实际浏览并阅读一手 arXiv 摘要及提交历史；部分打开论文 HTML 定位官方代码链接。**方法判断为摘要级核实，不表示全文精读、独立验证推理忠实性或实验复现。** 日期统一为 arXiv 首次提交日（UTC），分类是本仓库编辑建议。

## 可用于 README 的条目

| 首次提交 | 论文 | 任务 | 一句话贡献 | 建议主分类 / 标签 | 代码 |
| --- | --- | --- | --- | --- | --- |
| 2024-03-07 | **SLIM** — [Can Small Language Models be Good Reasoners for Sequential Recommendation?](https://arxiv.org/abs/2403.04260) | 序列推荐 | 把教师模型的逐步推理蒸馏给较小学生，并将学生生成的理由编码为推荐特征。 | 推理蒸馏与效率 / CoT、蒸馏 | 未核实 |
| 2024-05-17 | [RDRec: Rationale Distillation for LLM-based Recommendation](https://arxiv.org/abs/2405.10587) | Top-N、序列推荐 | 用大模型从评论提炼的推荐理由训练紧凑模型，增强用户和物品画像。 | 推理蒸馏与效率 / 理由蒸馏、画像 | [官方](https://github.com/WangXFng/RDRec) |
| 2024-08-12 | **EXP3RT** — [Review-driven Personalized Preference Reasoning with Large Language Models for Recommendation](https://arxiv.org/abs/2408.06276) | 评分预测、候选重排 | 蒸馏偏好提取、画像构建及逐步评分推理，让文本推理先于评分输出。 | 思维链与推理学习 / 评论、CoT、蒸馏 | [官方](https://github.com/jieyong99/EXP3RT) |
| 2025-03-28 | **ReaRec** — [Think Before Recommend: Unleashing the Latent Reasoning Power for Sequential Recommendation](https://arxiv.org/abs/2503.22675) | 序列推荐 | 反复回馈序列末端隐状态，以多步潜在推理细化用户表示。 | 推理时扩展 / 潜在推理、多步计算 | [官方](https://github.com/TangJiakai/ReaRec) |
| 2025-05-21 | [ThinkRec: Thinking-based recommendation via LLM](https://arxiv.org/abs/2505.15091) | 个性化推荐 | 注入合成推理轨迹，并按用户特征融合专家以适配个性化推理。 | 思维链与推理学习 / 合成轨迹、专家融合 | [官方](https://github.com/Yu-Qi-hang/ThinkRec) |
| 2025-06-05 | **R2Rec** — [Reason-to-Recommend: Using Interaction-of-Thought Reasoning to Enhance LLM Recommendation](https://arxiv.org/abs/2506.05069) | 基于交互的推荐 | 把用户—物品图中的交互链转为分步推理，先用轨迹监督学习，再用 RL 优化。 | 思维链与推理学习 / 交互图、CoT、SFT、RL | `https://anonymous.4open.science/r/R2Rec-7C5D`，内容未核实 |
| 2025-10-27 | **RecZero / RecOne** — [Think before Recommendation: Autonomous Reasoning-enhanced Recommender](https://arxiv.org/abs/2510.23077) | 评分预测 | 用结构化推理模板与 GRPO 联合优化推理轨迹和评分；同时研究 SFT 冷启动方案。 | 强化学习与奖励 / CoT、GRPO、冷启动 | [官方](https://github.com/AkaliKong/RecZero) |
| 2026-07-29 | [WhisperRec: Latent Reasoning for Efficient Foundation Recommendation Models](https://arxiv.org/abs/2607.26621) | 基础模型推荐 | 把教师 CoT 压缩为可学习潜在推理 token，减少显式理由生成的开销。 | 推理蒸馏与效率 / CoT 压缩、潜在推理 | 未核实 |

## 逐篇核实来源与收录依据

### 1. SLIM

- **核实层级：摘要级；另在全文 HTML 搜索代码链接。** [摘要及首次日期](https://arxiv.org/abs/2403.04260)；[论文 HTML](https://arxiv.org/html/2403.04260v2)。
- 属于推理增强：教师理由监督学生，学生理由的向量表示参与最终推荐；需要标明是“推理增强表示”，避免描述成直接生成物品 ID。
- 代码：本轮未找到论文给出的 SLIM 官方仓库；全文出现的 llama-recipes、SASRec 等是依赖或基线，不能当作 SLIM 代码。
- 发表状态：摘要页作者备注为 WWW 2024 已接收。

### 2. RDRec

- **核实层级：摘要级 + 官方仓库说明。** [摘要及首次日期](https://arxiv.org/abs/2405.10587) 直接链接 [WangXFng/RDRec](https://github.com/WangXFng/RDRec)，已打开且可见模型、蒸馏和评测文件。
- 属于推理增强：将交互背后的理由蒸馏到推荐模型；主归“理由蒸馏”。摘要不足以把它写成显式多步 CoT 决策。
- 评估注意：官方 README 的 Acknowledge 部分承认所用评论数据可能存在信息泄漏；不应直接摘取其最佳分数做跨论文排名。
- 发表状态：摘要页作者备注为 ACL 2024 Main short。

### 3. EXP3RT

- **核实层级：摘要级；全文摘要用于确认代码来源。** [摘要及首次日期](https://arxiv.org/abs/2408.06276)；[论文 HTML 摘要](https://arxiv.org/html/2408.06276v5) 明确链接 [jieyong99/EXP3RT](https://github.com/jieyong99/EXP3RT)，已打开并看到训练与推理说明。
- 属于推理增强：从评论构建偏好画像，逐步推理后才输出评分；兼有推理数据蒸馏和直接推理决策。
- 发表状态：摘要页作者备注为 SIGIR 2025 已接收。注意首稿是 2024 年。

### 4. ReaRec

- **核实层级：摘要级；全文实施细节用于确认代码来源。** [摘要及首次日期](https://arxiv.org/abs/2503.22675)；[论文 HTML §4.1.4](https://arxiv.org/html/2503.22675v3) 给出 [TangJiakai/ReaRec](https://github.com/TangJiakai/ReaRec)，已打开并看到源代码目录与启动说明。
- 属于推理增强：在推理时执行多步隐状态更新；归“潜在推理 / 推理时扩展”，不能描述成自然语言思维链。
- 评估注意：摘要中的 30%–50% 指事后分析的性能上限，不能当作普通部署设置的平均提升。
- 发表状态：arXiv 摘要未注明会议；官方仓库标题自述 TKDE '26。本笔记保留 arXiv 首稿日期，不用仓库标题替代正式出版核实。

### 5. ThinkRec

- **核实层级：摘要级 + 官方仓库。** [摘要及首次日期](https://arxiv.org/abs/2505.15091) 直接链接 [Yu-Qi-hang/ThinkRec](https://github.com/Yu-Qi-hang/ThinkRec)，已打开并确认有训练、推理和推理文本评价脚本。
- 属于推理增强：注入用户行为分析、偏好识别和目标物品判断的轨迹，推理本身是训练和推荐决策的一部分。
- 发表状态：摘要页作者备注为 WWW 2026。勿把 2026 年修订日期误当首次提交日期。

### 6. R2Rec

- **核实层级：摘要级。** [摘要及首次日期](https://arxiv.org/abs/2506.05069) 直接给出 `https://anonymous.4open.science/r/R2Rec-7C5D`。本轮打开只得到动态页面外壳，实际文件未核实。
- 属于推理增强：从交互图中抽取链作为推理依据，用渐进掩码提示构建轨迹，并通过 SFT 与 RL 学习逐步决策。
- 建议主归推理数据与学习，以 RL 为交叉标签，避免一篇在多个章节重复完整条目。
- 发表状态：已核实 arXiv 首次提交，其他发表状态未核实。

### 7. RecZero / RecOne

- **核实层级：摘要级；全文摘要用于确认代码来源。** [摘要及首次日期](https://arxiv.org/abs/2510.23077)；[论文 HTML 摘要](https://arxiv.org/html/2510.23077v1) 明确链接 [AkaliKong/RecZero](https://github.com/AkaliKong/RecZero)，已打开且可见 GRPO 脚本与训练框架。
- 属于推理增强：分析用户、分析物品、匹配、评分的结构化推理参与预测，并接受 RL 优化；不只是给推荐分数附加解释。
- RecZero 采用纯 RL，RecOne 采用冷启动 SFT 后 RL；它们属于同一篇论文，不应计为两篇。
- 发表状态：摘要页作者备注为 NeurIPS 2025 poster。

### 8. WhisperRec

- **核实层级：摘要级；另在全文 HTML 搜索代码链接。** [摘要及首次日期](https://arxiv.org/abs/2607.26621)；[论文 HTML](https://arxiv.org/html/2607.26621v2)。
- 属于推理增强：把多视角自适应 CoT 蒸馏到潜在 token，经对齐及课程式后训练激活推荐推理，以降低显式文本推理成本。
- 代码：本轮未找到作者提供的官方仓库，标“未核实”。
- 发表状态：已核实 arXiv 首次提交，其他发表状态未核实。摘要中的吞吐提升是作者报告，本轮不作独立性能背书。

## 编辑建议

- 主分类：思维链与推理学习放 EXP3RT、ThinkRec、R2Rec；RL 放 RecZero / RecOne；TTS 放 ReaRec；蒸馏与效率放 SLIM、RDRec、WhisperRec。
- 保留三种不同形态：**显式轨迹决策、理由增强表示、潜在多步推理**。不要因共同使用 “reasoning” 而抹平区别。
- 官方代码已核实 5 篇（RDRec、EXP3RT、ReaRec、ThinkRec、RecZero）；作者匿名链接内容未核实 1 篇（R2Rec）；代码未核实 2 篇（SLIM、WhisperRec）。全部代码均未运行。

## 后续链接核查

2026-09-15 的自动访问检查发现 R2Rec 作者匿名入口返回 401，SAPO 作者代码地址返回 404。原地址作为文字保留，不标为可用资源；详细记录见 [来源索引](../docs/sources.md#unavailable-resources)。
