# 基准与评测资源选型

[返回首页](../README.md) · [评测记录模板](evaluation.md) · [方法对照](method-matrix.md) · [前沿地图](frontier-map.md)

**核实日期：2026-09-15。** 这 6 个资源分别测量候选决策、交互可靠性、前提诊断、多任务能力、领域效用或模态证据。先按研究问题选协议，再比较模型；不要把它们汇总成一个没有任务说明的总榜。

## 六个官方资源

| 资源 | 候选空间与用户来源 | 约束 / 测量对象 | 主要指标 | 可用资源与边界 |
| --- | --- | --- | --- | --- |
| [τ-Rec](https://github.com/nbharaths/tau-rec) | 153 部电影目录，60 项任务；LLM 模拟用户 | 结构化属性约束、何时透露偏好、工具、策略遵守 | `pass^k` 连续成功可靠性；程序化校验 | 目录、任务、运行器、消融、轨迹和榜单；`g0`/`g1` 运行规范不同，作者明确不能直接混比 |
| [RPCBench](https://github.com/ZhongruChen/RPCBench) | 五域共 4,623 个合成并筛选的请求实例；可见证据快照 | 十类错误前提；候选不是统一排序池，重点是诊断请求 | Detection、Localization、Strategy、Faithfulness；三模型裁判 | 请求、提示、50,853 条被测响应、裁判聚合及分析；不能把裁判评分当客观约束验证 |
| [AgentRecBench](https://huggingface.co/datasets/SGJQovo/AgentRecBench) | 用户/物品/评论查询环境；每例 1 正 + 19 负；历史日志为真值 | 冷启动、长短期兴趣变化、数据可见性与工具规划 | HR@1、HR@3、HR@5 | 数据及[官方挑战环境](https://tsinghua-fib-lab.github.io/AgentSocietyChallenge/pages/overview.html)；不是实时真人满意度实验；数据浏览器当前解析报错不等于文件不可下载 |
| [RecIF-Bench / OpenOneRec](https://github.com/Kuaishou-OneRec/OpenOneRec) | 短视频/广告/商品的工业日志；全目录物品生成等多种任务，并非统一小候选池 | 八任务：语义对齐、预测、指令遵循、推荐解释 | Pass@1/32、Recall@32、AUC、LLM-as-Judge（随任务变化） | 数据处理、训练、评测、模型入口；解释得分不能证明推理对决策的因果贡献 |
| [Conv-FinRe](https://github.com/The-FinAI/Conv-FinRe) | 10 股票受控宇宙；真实行情与人类选择轨迹构成模拟咨询对话 | 行为模仿和拟合效用的分离；长期偏好、冲突建议 | uNDCG、MRR、HR@1/3、与专家排序的 Kendall τ | [数据集合](https://huggingface.co/collections/TheFinAI/conv-finre)、构造 notebooks、评测框架入口；效用函数是建模参照，非真实投资回报保证 |
| [MusiCRS](https://github.com/rohan2810/MusiCRS) | 477 条真实 Reddit 音乐对话；约 100 候选，含按赞数选出的最多 10 个正例 | 音频/文本/联合输入消融，跨模态证据使用 | Recall@K、nDCG@K、MRR 等 | [数据](https://huggingface.co/datasets/rohan2810/MusiCRS)、处理与基线脚本；音频通过 YouTube 链接关联，文件资源应单独核可用性 |

表格依据上述官方仓库或作者链接的数据卡；更细协议见 [AgentRecBench §4.4](https://arxiv.org/html/2505.19623v2)、[RecIF-Bench §3.1–3.3](https://arxiv.org/html/2512.24762v1)、[Conv-FinRe §3](https://arxiv.org/html/2602.16990v2)、[MusiCRS §2–3](https://arxiv.org/html/2509.19469v2)。

资源归属、读取版本和可用性详见 [本轮来源台账](../notes/frontier-agents-eval-2026-09-15.md)。数据卡或网页可访问，不表示全部媒体、运行依赖和下载文件已验证；本仓库尚未运行这些基准。

## 按实验问题选入口

| 你的问题 | 推荐起点 | 至少保留的控制组 |
| --- | --- | --- |
| 工具与规划是否提升给定候选决策 | AgentRecBench | 同候选、同证据的无工具/固定工具流程 |
| 多轮中能否持续满足用户约束 | τ-Rec | 相同运行规范与模拟器；重复运行；披露信息时机 |
| 模型能否发现请求中的错误前提 | RPCBench | 无错误前提请求；裁判家族与长度敏感性检查 |
| 方法能否接入开放推荐底座 | RecIF-Bench | 分任务报告；不要以解释得分代替决策因果验证 |
| 是否区分用户行为与模型化效用 | Conv-FinRe | 实际选择、效用与风险参照分别报告 |
| 音频证据是否改变推荐 | MusiCRS | 纯文本、纯音频、联合输入与冲突输入 |

表中是维护者的实验建议，不代表这些基准已经包含全部控制组。

## 两篇必须配套阅读的评测研究

### 候选、计分和解码会改变结论

[Retrieval, Scoring, and Decoding Shape Performance and Stability](../README.md#paper-crs-protocol) 比较受限候选重排、全目录评分和自由生成等协议。即使候选匹配，模型可访问的输入信息仍可能不同；该研究没有单独隔离 CoT。[证据卡](frontier-reading.md#crs-protocol)

**记录建议：** 单列候选召回率、条件重排指标和全链路指标；明确候选池是否包含强制插入的正例、负例如何采样，以及无效或目录外输出如何计分。

### 推理轨迹质量与推荐效果可能分离

[Descriptive Reasoning Disconnect](../README.md#paper-disconnect) 用表示与显式推理的控制实验区分轨迹描述质量和决策效果。[证据卡](frontier-reading.md#disconnect)

**记录建议：** 轨迹评分、最终决策和计算成本分栏，分别说明评分者、候选与预算。人工或 LLM 偏好不能自动替代基于目录事实的程序化校验。

## 最小报告清单

- **数据与版本**：数据集版本、时间切分、是否有跨切分评论/记忆、运行规范（例如 τ-Rec 的 g0/g1）。
- **信息与候选**：用户可见历史、工具目录、候选池、负例构造、目标是否强制进入候选。
- **交互来源**：历史日志、合成请求、模拟用户或真人；不要互换称谓。
- **指标定义**：K 的含义、聚合方式、失败样本是否保留、连续成功和至少一次成功的区别。
- **成本与稳定性**：训练、离线建库、在线模型/工具调用、token、平均及尾延迟、随机种子和重复运行差异。

直接填写 [评测模板](evaluation.md)，并附命令、固定提交和原始输出，才能将结果标为本仓库复现。
