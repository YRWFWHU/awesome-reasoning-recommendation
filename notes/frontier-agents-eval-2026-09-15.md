# 前沿补充：推荐智能体、可靠性与开放评测

核实日期：2026-09-15。范围：交互规划、工具推理、推理成本、推荐可靠性与专用评测资源。此文件为研究笔记；下面条目可以直接移入 README。所有论文已读 arXiv 一手摘要与首次提交记录；证据卡及基准细节另读指定版本全文。未运行作者实验，不将作者报告视为独立复现。

## 可直接采用的 9 篇新增条目

### NEXT: Reasoning-Driven Video Recommendation via a Vision-Language Model

**2026-06 · arXiv** · `视频推荐` `意图推理` `VLM` `离线挖掘` `线上A/B`

用“视频 → 下一兴趣意图 → 后续视频”的路径生成和验证推荐关系，把推理得到的关系作为工业系统的额外召回通道。VLM 主要在离线或近线运行；论文报告的线上收益属于整条召回路径，不宜直接归因于某一个推理训练阶段。

[论文](https://arxiv.org/abs/2607.24789) · 官方代码：未核实

### HARPO: Hierarchical Agentic Reasoning for User-Aligned Conversational Recommendation

**2026-04 · arXiv** · `会话推荐` `树搜索` `多维奖励` `偏好优化`

结合质量价值网络引导的推理树搜索、相关性与多样性等分层偏好目标，以及抽象工具操作和多智能体精炼。其 MUSE 实验将图像转为文字描述，应标为文本推理迁移，不能据此认定为原生视觉推理。

[论文](https://arxiv.org/abs/2604.10048) · [官方代码](https://github.com/harpo-bench/harpo-crs) · [项目页](https://harpo-bench.github.io/)

### AgenticRec: A Recommendation-Oriented Agentic Framework with Progressive Tool-Integrated Reasoning Optimization

**2026-03 · arXiv** · `工具推理` `GRPO` `困难负样本` `候选排序`

让用户画像、物品信息、行为统计和协同检索参与 Think–Act–Observation 决策循环；先以推荐反馈优化完整轨迹，再从排序错误挖掘难例进行双向偏好推理。实验采用 20 候选排序，不能直接推及全库召回。

[论文](https://arxiv.org/abs/2603.21613) · 作者匿名代码入口当前返回 403，内容未核实

### STAR: Internalizing Multi-Agent Reasoning for Accurate and Efficient LLM-based Recommendation

**2026-02 · arXiv** · `轨迹蒸馏` `协同证据` `工具调用` `GRPO`

多智能体教师把协同行为转为文字证据，学生通过筛选后的规划、工具和反思轨迹学习单智能体决策。论文报告学生超过教师并降低开销，但其延迟仍以秒计，不能把“效率提升”写成已满足实时推荐要求。

[论文](https://arxiv.org/abs/2602.09829) · 官方代码：未核实

### Retrieval, Scoring, and Decoding Shape Performance and Stability in LLM-based Conversational Recommendation

**2026-08 · arXiv** · `评测分析` `候选控制` `重排` `解码稳定性`

在 ReDial 上统一候选后比较 LLM 与传统重排器，分析候选生成、池大小、计分规则及温度如何改变结论。适合作为推理推荐的评测方法论：它不提出新的推理模型，也不单独证明 CoT 的有效或无效。

[论文](https://arxiv.org/abs/2609.00086) · [官方代码与输出](https://github.com/infobip/crs-performance)

### Conv-FinRe: A Conversational and Longitudinal Benchmark for Utility-Grounded Financial Recommendation

**2026-02 · arXiv** · `基准` `长期交互` `偏好推断` `多视角决策`

将实际选择、拟合效用、市场动量和风险偏好设为不同参照，检验对话推荐是否只是在模仿行为。真实行情及人类决策轨迹用于构造受控对话；效用参照来自模型假设，不能当作客观、唯一的用户最优决策。

[论文](https://arxiv.org/abs/2602.16990) · [官方代码](https://github.com/The-FinAI/Conv-FinRe) · [官方数据集合](https://huggingface.co/collections/TheFinAI/conv-finre)

### OpenOneRec Technical Report / RecIF-Bench

**2025-12 · arXiv** · `基准` `开放模型` `指令遵循` `多任务`

发布跨短视频、广告与商品的八任务评测、训练数据与推荐基础模型。收录价值在开放研究底座；其“推理”任务主要是推荐解释，因此八任务总分不等价于推理轨迹的因果忠实性。

[论文](https://arxiv.org/abs/2512.24762) · [官方代码、评测与资源入口](https://github.com/Kuaishou-OneRec/OpenOneRec)

### MusiCRS: Benchmarking Audio-Centric Conversational Recommendation

**2025-09 · arXiv** · `基准` `音频依据` `会话推荐` `模态消融`

把真实音乐讨论与音频关联，对比音频、文本及二者结合的推荐能力。它补足“偏好推理是否使用了声音证据”的评测入口，但本身不是 CoT 忠实性或强化学习基准。

[论文](https://arxiv.org/abs/2509.19469) · [官方代码](https://github.com/rohan2810/MusiCRS) · [官方数据](https://huggingface.co/datasets/rohan2810/MusiCRS)

### AgentRecBench: Benchmarking LLM Agent-based Personalized Recommender Systems

**2025-05 · arXiv** · `基准` `工具环境` `冷启动` `兴趣变化`

提供可查询的用户、评论与物品环境，评估普通推荐、用户或物品冷启动以及兴趣变化。虽然名为交互模拟环境，主要结果仍按历史真实物品的 20 候选命中率评测，不能解释为真实用户会话满意度。

[论文](https://arxiv.org/abs/2505.19623) · [官方数据](https://huggingface.co/datasets/SGJQovo/AgentRecBench) · [作者挑战与环境入口](https://tsinghua-fib-lab.github.io/AgentSocietyChallenge/pages/overview.html)

## 证据卡：推荐采用 3 篇

### STAR：蒸馏收益和部署延迟应分开读

**机制与证据。** 教师的多智能体轨迹经过结果筛选后，学生进行 SFT 与 GRPO；工具调用标记仍保留。AgentRecBench 采用一正例加 19 个随机负例，表中主指标为 HR@1/3/5 的平均值。Goodreads 五场景平均分从教师 66.2 到学生 78.4；去除 GRPO 后为 75.5，去除反思后为 71.9。

**成本与边界。** Limitations 报告学生 89 秒、教师 461 秒，且明确未满足亚秒级服务；离线文字证据还增加存储成本。该实验支持给定候选条件下的蒸馏收益，未验证全库检索。

来源：[v2 全文 §3.4、§4.1、Table 2、Limitations](https://arxiv.org/html/2602.09829v2)。

### HARPO：搜索有代价，多模态结论有边界

**机制与证据。** 价值网络引导树搜索，分层偏好奖励和工具操作共同参与训练。ReDial 消融中完整模型 R@10 为 29.8%，移除树搜索模块为 27.0%；作者注明组件消融会重训，因此不能将全部差值解释为预测时搜索本身的独立贡献。评测在每正例搭配 99 个负例的候选集上进行。

**成本与边界。** Table 12 报告每轮 298 ms，去搜索为 88 ms；数字是作者特定设置的测量，不能横向比较其他论文。MUSE 输入使用 BLIP-2 的文字描述，且正式去污染分析仍属未来工作。

来源：[v2 全文 Table 4、Appendix D.2/D.5、E.3/E.4](https://arxiv.org/html/2604.10048v2)。

### CRS performance：先控制候选，再讨论模型强弱

**协议与证据。** 在 ReDial 的 1,025 个测试对话上固定语义 top-250 候选，最强闭源重排器 NDCG@10 为 0.1497，EASE 为 0.0939；同一 LLM 在无候选限制的生成计分下为 0.2925。这些设置的物品访问范围不同，不能放在同一排行榜比较。升温时平均准确率可能近似不变，但 top-10 集合不一致性仍增加。

**边界。** 这是单数据集的系统比较；作者强调候选匹配没有使输入信息相同：LLM 有原始对话和预训练知识，传统模型主要用交互。没有单独隔离 CoT，也没有提供同预算推理收益结论。

来源：[v1 全文 §2–4](https://arxiv.org/html/2609.00086v1)；[公开提示、配置与输出](https://github.com/infobip/crs-performance)。

## 可加入方法对照矩阵的字段

| 工作 | 推理对象与形式 | 训练信号 | 推理发生位置 | 已核验的评测范围 | 成本或关键限制 |
| --- | --- | --- | --- | --- | --- |
| STAR | 协同证据、规划、工具、反思轨迹 | 筛选轨迹 SFT + GRPO | 单智能体生成与工具 | AgentRecBench；20 候选；HR@1/3/5 平均 | 89 s 对教师 461 s；非亚秒级 |
| HARPO | 会话偏好、价值网络引导推理树、抽象工具操作 | 分层偏好优化与多阶段训练 | 对话轮次中的搜索 | ReDial/INSPIRED/MUSE；100 候选 | 每轮 298 ms 对无搜索 88 ms；MUSE 用文字代理 |
| AgenticRec | Think–Act–Observation；难候选双向比较 | GRPO + 排序难例反馈 | 在线工具推理循环 | Amazon 四子域；20 候选；HR/NDCG | 单 A800 平均每请求 16.233–20.678 s；最多 10 次工具交互 |
| NEXT | 视频证据 → 下一意图 → 候选验证 | 感知 RL、SFT、GRPO | 离线/近线关系挖掘，线上关系召回 | 1,000 视频的 LLM judge + 线上 A/B | 作者报告 watch time +0.53%；未隔离各阶段因果贡献；全库挖掘仍昂贵 |
| CRS performance | 评测协议，非新推理方法 | 多类模型比较 | 重排、解码与计分 | ReDial；c250/c500/c1000/全目录/无候选 | 必须标候选可见性与计分；输入信息仍不同 |

矩阵事实来源：[STAR 全文](https://arxiv.org/html/2602.09829v2)、[HARPO 全文](https://arxiv.org/html/2604.10048v2)、[AgenticRec v2 §5.4/Table 3/Appendix C.1](https://arxiv.org/html/2603.21613v2)、[NEXT v1 §5/Limitations](https://arxiv.org/html/2607.24789v1)、[协议研究 v1](https://arxiv.org/html/2609.00086v1)。数值仅在各自协议内可比。

## 六个官方评测资源入口及选择依据

这里包含已有 τ-Rec/RPCBench 的资源深化，不将它们再次计为新增论文。

| 资源 | 候选空间与用户来源 | 约束 / 测量对象 | 主要指标 | 可用资源与边界 |
| --- | --- | --- | --- | --- |
| [τ-Rec](https://github.com/nbharaths/tau-rec) | 153 部电影目录，60 项任务；LLM 模拟用户 | 结构化属性约束、何时透露偏好、工具、策略遵守 | `pass^k` 连续成功可靠性；程序化校验 | 目录、任务、运行器、消融、轨迹和榜单；`g0`/`g1` 运行规范不同，作者明确不能直接混比 |
| [RPCBench](https://github.com/ZhongruChen/RPCBench) | 五域共 4,623 个合成并筛选的请求实例；可见证据快照 | 十类错误前提；候选不是统一排序池，重点是诊断请求 | Detection、Localization、Strategy、Faithfulness；三模型裁判 | 请求、提示、50,853 条被测响应、裁判聚合及分析；不能把裁判评分当客观约束验证 |
| [AgentRecBench](https://huggingface.co/datasets/SGJQovo/AgentRecBench) | 用户/物品/评论查询环境；每例 1 正 + 19 负；历史日志为真值 | 冷启动、长短期兴趣变化、数据可见性与工具规划 | HR@1、HR@3、HR@5 | 数据及[官方挑战环境](https://tsinghua-fib-lab.github.io/AgentSocietyChallenge/pages/overview.html)；不是实时真人满意度实验；数据浏览器当前解析报错不等于文件不可下载 |
| [RecIF-Bench / OpenOneRec](https://github.com/Kuaishou-OneRec/OpenOneRec) | 短视频/广告/商品的工业日志；全目录物品生成等多种任务，并非统一小候选池 | 八任务：语义对齐、预测、指令遵循、推荐解释 | Pass@1/32、Recall@32、AUC、LLM-as-Judge（随任务变化） | 数据处理、训练、评测、模型入口；解释得分不能证明推理对决策的因果贡献 |
| [Conv-FinRe](https://github.com/The-FinAI/Conv-FinRe) | 10 股票受控宇宙；真实行情与人类选择轨迹构成模拟咨询对话 | 行为模仿和拟合效用的分离；长期偏好、冲突建议 | uNDCG、MRR、HR@1/3、与专家排序的 Kendall τ | [数据集合](https://huggingface.co/collections/TheFinAI/conv-finre)、构造 notebooks、评测框架入口；效用函数是建模参照，非真实投资回报保证 |
| [MusiCRS](https://github.com/rohan2810/MusiCRS) | 477 条真实 Reddit 音乐对话；约 100 候选，含按赞数选出的最多 10 个正例 | 音频/文本/联合输入消融，跨模态证据使用 | Recall@K、nDCG@K、MRR 等 | [数据](https://huggingface.co/datasets/rohan2810/MusiCRS)、处理与基线脚本；音频通过 YouTube 链接关联，文件资源应单独核可用性 |

基准表依据：上述官方仓库或作者链接的数据卡；更细协议见 [AgentRecBench §4.4](https://arxiv.org/html/2505.19623v2)、[RecIF-Bench §3.1–3.3](https://arxiv.org/html/2512.24762v1)、[Conv-FinRe §3](https://arxiv.org/html/2602.16990v2)、[MusiCRS §2–3](https://arxiv.org/html/2509.19469v2)。

## 元信息、资源溯源与易错点

| 简称 | arXiv ID | 首次提交（UTC） | 核读版本 | 官方资源来源 |
| --- | --- | --- | --- | --- |
| STAR | 2602.09829 | 2026-02-10 | v2 | 未从论文确认官方代码 |
| HARPO | 2604.10048 | 2026-04-11 | v2 | 全文链接 harpo-bench.github.io，项目页 Code 跳转 harpo-bench/harpo-crs；已打开目标仓库 |
| AgenticRec | 2603.21613 | 2026-03-23 | v2 | 摘要指定 anonymous.4open.science/r/AgenticRec-FB16；HTTP 403，内容未确认 |
| NEXT | 2607.24789 | 2026-06-27 | v1 | 未从论文确认官方代码 |
| CRS performance | 2609.00086 | 2026-08-31 | v1 | 全文脚注直接指向 infobip/crs-performance，已打开 |
| AgentRecBench | 2505.19623 | 2025-05-26 | v2 | 摘要直接给数据与挑战站点，均已打开 |
| OpenOneRec | 2512.24762 | 2025-12-31 | 摘要 v2、协议全文 v1 | 全文首页指向 Kuaishou-OneRec/OpenOneRec，已打开；未把 v1 全文误写成 v2 |
| Conv-FinRe | 2602.16990 | 2026-02-19 | v2 | 全文脚注直接给 The-FinAI 仓库与数据集合，均已打开 |
| MusiCRS | 2509.19469 | 2025-09-23 | v2 | 摘要直接给 rohan2810 仓库与数据，均已打开 |

日期经 arXiv 提交页及 `citation_date` 元数据交叉核实。NEXT、CRS performance 的首次月份与 ID 前缀不一致，沿用仓库“首次提交月份”口径；AgenticRec v1 标题是 *End-to-End Tool-Integrated Policy Optimization for Ranking-Oriented Recommender Agents*，当前 v2 已更名，不应按两篇计数。

## 可用于研究地图的判断（编辑分析）

1. **推理应与信息获取一起评估。** 工具推荐改善可能来自新证据、训练或计算，应分别设置无工具、同证据、同候选和同预算对照。
2. **开放基准关注不同层面。** AgentRecBench 测给定候选决策，τ-Rec 测交互约束可靠性，RPCBench 测错误前提处理，MusiCRS 测跨模态依据，RecIF 测工业任务覆盖，Conv-FinRe 测行为与效用的冲突；不宜合成一个无协议说明的统一总榜。
3. **效率要报告绝对值。** STAR 与 AgenticRec 均说明“减少开销”不意味着毫秒级在线排序；NEXT 说明可以将昂贵推理移至离线关系构造。
4. **可靠性不等同于平均准确率。** 应同时记录重复生成的一致性、约束违反、推理证据忠实性、隐藏偏好的获取效率及候选池之外的输出处理。

## 未采用候选

- [Retrieval over Reasoning: A Cost-Controlled Benchmark of Language Models for Energy-Retrofit Recommendation](https://arxiv.org/abs/2607.05440)：有检索/推理正交消融与成本比较价值，但属建筑节能措施分类，离本仓库用户偏好推荐主线较远，本次不占核心条目。
- 通用 Agent Planning Benchmark、Plan-RewardBench 等：可供方法论借鉴，但不是推荐专用资源，未用于补足论文数量。
