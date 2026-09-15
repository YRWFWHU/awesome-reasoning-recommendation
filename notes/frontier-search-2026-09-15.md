# 前沿扩展：检索范围与新增来源

检索截止：2026-09-15。主题为推理增强推荐，优先补齐 2026 年工作，尤其近期的潜在推理、预算控制、过程奖励、推理内化与评测证据；同时补充影响后续路线的早期工作。

## 检索方式

- 通过 arXiv、Hugging Face Papers、作者项目及综述配套列表发现候选。
- 示例检索式：`reasoning recommendation`、`recommendation reasoning 2608`、`recommendation reasoning 2609`、`reasoning recommendation survey`、`latent reasoning recommendation`。
- 对候选逐篇打开一手摘要与提交历史；关键结论继续追方法、消融、成本或评测章节。
- 日期取页面记载的首次提交时间，不从 arXiv 编号推断具体提交日，也不把修订日期当成首稿日期。
- 代码必须能沿论文或作者页面追溯；无法访问时记录结果，不把占位仓库标成可复现实现。

这是有明确范围的精选检索，不是对所有学术数据库的系统综述，也不保证穷尽截止日之前的论文。收录年份不代表研究质量，预印本的新结论需持续核对。

## 分专题证据

- [CoT、潜在推理与蒸馏](frontier-cot-latent-2026-09-15.md)
- [RL、搜索与推理时预算](frontier-rl-tts-2026-09-15.md)
- [智能体、交互与评测](frontier-agents-eval-2026-09-15.md)

## 本页补充核实

### SelfDR

- 标题：SelfDR: Self-Distillation from Reasoning for LLM-Based Recommendation。
- 首次提交：2026-09-03；[一手摘要](https://arxiv.org/abs/2609.03313)。
- 机制：同一基座构建推理器、带理由的教师及直接推荐学生；下游奖励训练推理器，动态加权蒸馏教师预测。
- 已局部读取：[§3](https://arxiv.org/html/2609.03313v1#S3)、[§4.4–4.5](https://arxiv.org/html/2609.03313v1#S4.SS4)。效率实验以单 A800 上 Clothing 的 2,000 个样本统计，不可外推为任意硬件或全库端到端时延。
- [作者代码](https://github.com/JiangDeccc/SelfDistillation) 由摘要直接链接且页面可见；未运行。

### Descriptive Reasoning Disconnect

- 标题：The Disconnect Between Better Descriptive Reasoning Trace Quality and Recommendation Effectiveness。
- 首次提交：2026-08-24；[一手摘要](https://arxiv.org/abs/2608.23154)。
- 已局部读取：[§3–5](https://arxiv.org/html/2608.23154v1#S3)、[§6](https://arxiv.org/html/2608.23154v1#S6)。2×2 主设计比较物品表示（SID/Title）与显式推理（有/无），另研究更充分的 SID 对齐；不是“表示×对齐程度”的主因子设计。
- 研究范围：共享 Qwen3-1.7B、三个 Amazon 领域及文中离线协议。轨迹描述质量与离线效果可能分离，不能推导成所有推荐推理都无效。
- 官方代码未核实。

### Agentic Recommender Roadmap

- 标题：Autonomous Information Seeking: A Roadmap for Agentic Recommender Systems。
- 首次提交：2026-07-05；[一手摘要](https://arxiv.org/abs/2607.04433)。
- 核实层级：摘要及正文目录。覆盖智能体辅助推荐、作为推荐器和作为用户模拟器等角色，以及轨迹评估和模拟器校准问题。
- 作为综述导航单列，不计作提出新方法或新基准。

## 如何使用研究建议

[前沿研究地图](../docs/frontier-map.md) 中的实验建议是维护者根据来源提出的可检验问题，不代表原作者已完成这些实验，也不声称这些问题尚未被任何其他论文研究。具体方法差异与证据范围见 [方法对照表](../docs/method-matrix.md)。
