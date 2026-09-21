# 来源与核实记录

[返回首页](../README.md)

核实日期：2026-09-15。通过一手论文页面核实标题、arXiv 首次提交时间和主要方法；有官方资源时沿论文或作者页面核对归属。链接检查只验证访问和锚点，不验证论文结论。

## 核实层级

| 层级 | 实际做了什么 | 没有据此声称什么 |
| --- | --- | --- |
| 摘要核实 | 阅读一手摘要、核对标题与提交记录 | 全文精读、结果独立验证 |
| 正文局部核实 | 阅读相关方法、实验、消融或成本章节 | 对论文全部细节作出结论 |
| 官方资源核实 | 从作者来源追踪链接，并打开资源页面 | 已运行代码、已下载全部数据 |
| 实验复现 | 记录环境、命令、日志与指标 | 本仓库尚未开展 |

## 覆盖记录

| 条目 | 核实层级 | 记录 |
| --- | --- | --- |
| OneRec-Think、GR2、OneReason、TTR | 摘要与正文局部；OneRec-Think 另核官方仓库 | [精选阅读卡片](reading-notes.md) |
| SLIM、RDRec、EXP3RT、ReaRec、ThinkRec、R2Rec、RecZero/RecOne、WhisperRec | 摘要；部分正文代码链接及官方资源 | [思维链与蒸馏来源笔记](../notes/research-cot-distillation.md) |
| AgentDR、MGFRec、SAPO、RPORec、ReasonRec、τ-Rec、RPCBench、PROMISE、Rec-R1 | 摘要；部分正文和官方资源；AgentDR 有局部深入核实 | [RL、TTS 与智能体来源笔记](../notes/research-rl-tts.md) |
| TIGER、OneRec | 摘要与提交记录，作为背景 | [最初范围调研](../notes/scope-research.md) |
| LatentR³、FLR、IntuRec、IBA、LaRec、HiLaR、EvoReason、rEDMRec | 全部摘要；6 篇另读局部章节；代码状态分别记录 | [潜在推理来源](../notes/frontier-cot-latent-2026-09-15.md) |
| ReRec、SIDReasoner、ManCAR、R2Rank、EGLR、DTRec、GREAM、RecLLM-R1、R²ec | 全部摘要；部分方法/消融/预算章节 | [RL 与预算来源](../notes/frontier-rl-tts-2026-09-15.md) |
| STAR、HARPO、AgenticRec、NEXT、AgentRecBench、OpenOneRec、Conv-FinRe、MusiCRS、CRS 协议研究 | 全部摘要；局部正文、基准协议与官方资源 | [智能体与基准来源](../notes/frontier-agents-eval-2026-09-15.md) |
| SelfDR、Disconnect、Agentic Roadmap | 前两篇局部方法/实验；Roadmap 摘要与目录 | [本轮检索记录](../notes/frontier-search-2026-09-15.md) |

月份取首次提交记录，方法摘要以本次读取版本为依据。需讨论实验细节时，使用阅读卡片中的固定版本链接；首页论文链接指向 arXiv 当前版本。

## 前沿扩展的组织方式

本轮新增 29 篇，总计 52 篇。新增材料连接到 [研究地图](frontier-map.md)、[28 方法对照](method-matrix.md)、[6 个基准选型](benchmarks.md) 和 [12 篇前沿证据卡](frontier-reading.md)。加上原有 5 篇卡片，共 17 篇精选卡片；来源笔记中其他短评不重复计入。

## 需要保留的限定

- **RDRec：** 官方仓库提示评论数据可能泄漏，不能省略这一说明。
- **ReaRec：** 摘要中的较大上限来自事后分析，不等于普通推理策略的平均收益。
- **OneReason：** 正文同时讨论 thinking/non-thinking；结论依赖训练设置、领域与指标。
- **AgentDR：** 记忆更新之后的列表生成耗时不包含全部前置推理。
- **SAPO、R2Rec：** 已定位作者资源入口，但本轮访问分别返回 404 和 401，详见下方记录。
- **HiLaR：** 官方仓库目前只有占位 README，不能标为可复现实现。
- **STAR、HARPO、NEXT：** 分别注意绝对延迟、文字化图像输入和离线关系挖掘，不能混作在线原生多模态推理。
- **GREAM、EGLR、ManCAR：** 训练扩展、预测预算、不同指标和不同预算的比较需要分别记录。
- **PROMISE：** 归入结构化路径搜索；不将语义 ID 前缀写成自然语言思维链。

<a id="unavailable-resources"></a>
## 当前无法访问的作者资源

2026-09-15 使用 lychee 0.24.2 或 HTTP 请求检查时，以下地址未通过访问检查。保留原地址用于后续追踪，首页不将它们作为可用代码链接：

| 论文 | 作者给出的地址 | 本次结果 |
| --- | --- | --- |
| [R2Rec](https://arxiv.org/abs/2506.05069) | `https://anonymous.4open.science/r/R2Rec-7C5D` | 重定向后的接口返回 401；内容未核实 |
| [SAPO](https://arxiv.org/abs/2605.17648) | `https://github.com/zhengzaiyi/SAPO` | 返回 404；公开实现未核实 |
| [AgenticRec](https://arxiv.org/abs/2603.21613) | `https://anonymous.4open.science/r/AgenticRec-FB16` | HTTP 请求返回 403；内容未核实 |

此记录描述本次访问结果，不推断作者未发布资源。若后续恢复或迁移，核对作者归属后再补回链接。

## 纠错与更新

来源变更、论文修订或官方实现发布后，请同时更新首页与相应记录。保留“作者报告”和“维护者解读”的区别；纠错入口见 [贡献指南](../CONTRIBUTING.md)。

## 2026-09-15：潜在推理与 SID 交叉补录

在上一轮52篇的基础上，新增 **29篇**：首批11篇与逐主张查新追加18篇。其中22篇核心方法、4篇评测研究、3篇必要背景；当前总计 **81篇**。原有17篇精选卡片保持不变。首次日期、版本、核读深度和资源状态见 [逐篇补录记录](../notes/latent-sid-search-2026-09-15.md)。

本次来自研究idea阶段的文献回流，按照 [文献核实与去重流程](../CONTRIBUTING.md) 执行；未发表的研究候选与内部审查记录保留在本地。

## 2026-09-17 潜在推理定向更新

新增 LARK 1 篇，总计82篇（63核心、6基准、6评测、1综述、6背景）。已核对一手摘要、2026-09-04首次提交记录及正文§3.4：在线使用预计算物品表示，不将其归为在线SID生成。资源归属与实现仍未核实。其余本轮核对的代表方法已收录，未重复添加。见[本轮来源笔记](../notes/latent-reasoning-update-2026-09-17.md)。

## 2026-09-17 研究缺口检索回流

另补OnePiece、ENF两篇既有相关工作，当前84篇（65核心、6基准、6评测、1综述、6背景），不是两篇刚发表的新论文。核实一手摘要与首次日期，不宣称全文复现；Expl-Debias留待核实。见[来源与范围记录](../notes/latent-open-questions-2026-09-17.md)。

## 2026-09-17 方法选题补充

新增EPIC、MoMoREC、MindRec三篇核心与MDGR、MADRec/MaskGR、TCA4Rec三篇必要背景，更新OneRec-Think正式ACL链接；总90篇（68核心、6基准、6评测、1综述、9背景）。见[逐篇证据与范围](../notes/method-ideation-sources-2026-09-17.md)。

## 2026-09-19 HiLaR奖励口径核对

细化已有HiLaR条目：平均token对数概率、裁剪与层级权重、协同偏好奖励，以及物品标题生成和用户偏好量化的区别。新增0篇，总90篇不变。见[正文核实记录](../notes/hilar-reward-verification-2026-09-19.md)。

## 2026-09-21 每周检查

本轮从2026-09-15基准向前重叠14天，覆盖2026-09-01至09-21 01:10 UTC。新增7篇（6核心、1评测），总97篇（74核心、6基准、7评测、1综述、9背景）；精选卡片仍为17篇。新增Re2A、NarraLite、P³Rec、LIGE-GR、Trade-Up蒸馏、AtomRec和UPR画像干预评测，更新TGR的训练监督与部署边界。SARA留作边界候选。首次日期、固定版本、资源状态、排除理由与证据限定见[周检记录](../notes/weekly-search-2026-09-21.md)。
