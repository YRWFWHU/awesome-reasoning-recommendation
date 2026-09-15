# 来源与核实记录

[返回首页](../README.md)

核实日期：2026-09-15。首版通过一手论文页面核实标题、arXiv 首次提交时间和主要方法；有官方资源时沿论文或作者页面核对归属。链接检查只验证访问和锚点，不验证论文结论。

## 核实层级

| 层级 | 实际做了什么 | 没有据此声称什么 |
| --- | --- | --- |
| 摘要核实 | 阅读一手摘要、核对标题与提交记录 | 全文精读、结果独立验证 |
| 正文局部核实 | 阅读相关方法、实验、消融或成本章节 | 对论文全部细节作出结论 |
| 官方资源核实 | 从作者来源追踪链接，并打开资源页面 | 已运行代码、已下载全部数据 |
| 实验复现 | 记录环境、命令、日志与指标 | 首版尚未开展 |

## 覆盖记录

| 条目 | 核实层级 | 记录 |
| --- | --- | --- |
| OneRec-Think、GR2、OneReason、TTR | 摘要与正文局部；OneRec-Think 另核官方仓库 | [精选阅读卡片](reading-notes.md) |
| SLIM、RDRec、EXP3RT、ReaRec、ThinkRec、R2Rec、RecZero/RecOne、WhisperRec | 摘要；部分正文代码链接及官方资源 | [思维链与蒸馏来源笔记](../notes/research-cot-distillation.md) |
| AgentDR、MGFRec、SAPO、RPORec、ReasonRec、τ-Rec、RPCBench、PROMISE、Rec-R1 | 摘要；部分正文和官方资源；AgentDR 有局部深入核实 | [RL、TTS 与智能体来源笔记](../notes/research-rl-tts.md) |
| TIGER、OneRec | 摘要与提交记录，作为背景 | [最初范围调研](../notes/scope-research.md) |

月份取首次提交记录，方法摘要以本次读取版本为依据。需讨论实验细节时，使用阅读卡片中的固定版本链接；首页论文链接指向 arXiv 当前版本。

## 需要保留的限定

- **RDRec：** 官方仓库提示评论数据可能泄漏，不能省略这一说明。
- **ReaRec：** 摘要中的较大上限来自事后分析，不等于普通推理策略的平均收益。
- **OneReason：** 正文同时讨论 thinking/non-thinking；结论依赖训练设置、领域与指标。
- **AgentDR：** 记忆更新之后的列表生成耗时不包含全部前置推理。
- **SAPO、R2Rec：** 已定位作者资源入口，但本轮访问分别返回 404 和 401，详见下方记录。
- **PROMISE：** 归入结构化路径搜索；不将语义 ID 前缀写成自然语言思维链。

<a id="unavailable-resources"></a>
## 当前无法访问的作者资源

2026-09-15 使用 lychee 0.24.2 检查时，以下地址未通过访问检查。保留原地址用于后续追踪，首页不将它们作为可用代码链接：

| 论文 | 作者给出的地址 | 本次结果 |
| --- | --- | --- |
| [R2Rec](https://arxiv.org/abs/2506.05069) | `https://anonymous.4open.science/r/R2Rec-7C5D` | 重定向后的接口返回 401；内容未核实 |
| [SAPO](https://arxiv.org/abs/2605.17648) | `https://github.com/zhengzaiyi/SAPO` | 返回 404；公开实现未核实 |

此记录描述本次访问结果，不推断作者未发布资源。若后续恢复或迁移，核对作者归属后再补回链接。

## 纠错与更新

来源变更、论文修订或官方实现发布后，请同时更新首页与相应记录。保留“作者报告”和“维护者解读”的区别；纠错入口见 [贡献指南](../CONTRIBUTING.md)。
