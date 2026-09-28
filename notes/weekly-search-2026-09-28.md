# 2026-09-28 每周文献检查

[返回首页](../README.md) · [来源总表](../docs/sources.md)

## 检索窗口与执行范围

- 接续上次完整周检截止 **2026-09-21 01:10 UTC**，本次查询窗口 **2026-09-07 00:00 至 2026-09-28 01:01 UTC**，重叠超过14天。9月21日的综述定向补录不替代完整周检。
- 发现阶段以104篇清单为基线，先读 README、贡献规范与上周记录，按标题及 arXiv ID 去重。使用 research 技能分工核实；本页记录公开资料阅读，不是实验复现。
- 实际调用 arXiv API：`(all:recommendation OR all:recommender) AND (all:reasoning OR all:latent OR all:distillation OR all:reward OR all:"test-time") AND lastUpdatedDate:[202609070000 TO 202609280101]`，按最近修订降序，`max_results=200`，HTTP 200、61条；补充不设机制关键词的 `(ti:recommendation OR ti:recommender) AND lastUpdatedDate:[202609070000 TO 202609280101]`，HTTP 200、86条。两批互有重合，不相加为独立论文数。
- 补充网页查询包括 arXiv + recommendation/reasoning/latent/distillation/test-time + September 2026，以及固定标题查询。索引可延迟；空查询不代表不存在论文。非一手列表和新闻仅作发现，不作为收录依据。
- 原始查询参数、完整返回元数据与摘要保存在本地研究目录 `literature/WEEKLY_DISCOVERY_20260928.json`。公开条目依据下列固定论文版本及作者资源。

## 方法类核实

| 工作 | 首次提交（UTC）与版本 | 核读深度与收录依据 | 资源状态 |
| --- | --- | --- | --- |
| Evo-Rec：Learning Better Reasoning for Generative Recommendation with Semantic IDs | [2026-09-24 15:24:54；v1](https://arxiv.org/abs/2609.29973) | [v1 §3.3–3.4、§4.1–4.3](https://arxiv.org/html/2609.29973v1)：按目标SID概率增益选择显式轨迹，再用目录约束beam的目标排名奖励优化；归思维链与推理学习。 | [作者仓库](https://github.com/mengdanzhu/evo-rec)含三阶段与评测脚本；README明确部分训练/验证数据及通用推理数据待发布，不能称完整复现包。 |
| From Interests to Semantic IDs: Retrieval-Grounded Credit Assignment for Generative Recommendation | [2026-09-24 15:34:11；v1](https://arxiv.org/abs/2609.29983) | [v1 PDF §3、§4.1–4.5](https://arxiv.org/pdf/2609.29983v1)：冻结检索器逐兴趣查询查目标，把检索优势分配至对应兴趣文本，而非最终SID；归强化学习与奖励。HTML访问失败后改读PDF。 | [作者仓库](https://github.com/YuFan-Microsoft/Retrieval-Grounded-Credit-Assignment-for-Generative-Recommendation)含训练、检索与评测实现；README要求本地数据文件，没有配置远端数据仓库；未运行。 |
| Generative Query Suggestion via Intent Coverage and Query-Level Credit Assignment | [2026-09-16 11:19:06；v1](https://arxiv.org/abs/2609.19209) | [v1 §3–4](https://arxiv.org/html/2609.19209v1)：会话后续问题推荐，混合CoT/直接生成SFT，再结合查询级质量优势与列表级意图覆盖；归强化学习与奖励并标任务边界。 | 论文未核实到官方代码入口；工业数据，不声称公开可复现。 |

### 证据限定

- **Evo-Rec：** 训练每例5个教师轨迹、RL每组16条，预测在全目录trie上beam=10。基线数值引用SIDReasoner而非本仓库重跑。式6的exact-match是top-1，§4.3.3文字却描述top-10命中，故不据该消融推断精确奖励效应；目标概率增益也不等于语义正确性。[v1 §3–4](https://arxiv.org/html/2609.29973v1)
- **检索归因：** 主评测是全目录beam=10；默认奖励检索为Qwen3-Embedding-4B、top-50，不能混成50候选主协议。图5用目标选择兴趣的oracle仅为上界。I-R@50沿用奖励检索器，不构成独立检索泛化。检索负例轨迹的负优势在其有效兴趣间分摊；不能概括为只奖不罚或不压制未点击兴趣。论文表5比较广播、兴趣块及命中查询归因，但没有证明多偏好效用正确性。[v1 §3.3、§4.1–4.5](https://arxiv.org/pdf/2609.29983v1)
- **后续问题推荐：** SFT含20%意图CoT与80%直接生成；奖励赋给输出查询片段，不是逐个中间推理步骤。作者将意图覆盖和LLM裁判视为与训练目标对齐的诊断，主要独立证据为CTR和人工GSB；线上绝对CTR和流量数未公开。不将其等同SID物品推荐或独立过程忠实性评测。[v1 §3.2–4.3](https://arxiv.org/html/2609.19209v1)

## 暂缓与范围外

- [TATK，2609.14565v1](https://arxiv.org/html/2609.14565v1)，首次09-13。核读§3–4及[作者代码入口](https://github.com/conor1020/TATK)。是元数据图注入与top-100候选图分数重排，明确无需CoT或额外LLM步骤；与Reason4Rec的对照改为单pass、不含其原多步专家流程。保留为结构验证对照候选，不能因verifier名称自动归推理核心。
- [SARA，2609.17639v2](https://arxiv.org/html/2609.17639v2)，首次09-15、09-21修订。复查§2.3、§5，仍将作者侧正负理由作为排序特征/量化特征；未建立多步推理或轨迹蒸馏依据，延续待核边界，不新增计数。
- [ReliGRec，2609.16560v1](https://arxiv.org/html/2609.16560v1)，首次09-15。核读Methodology的prompt routing及RQ3：两提示都仅输出一个SID、不生成中间分析；风险条件提示不等于已核推理机制。暂不纳核心。
- [OneLA，2609.12399v1](https://arxiv.org/abs/2609.12399)，首次09-11。摘要核实是大beam线性注意力状态共享与系统加速，不独立建立推理/预算分配机制；不因large beam自动收核心。
- [Complete Suffix Prediction，2609.15692v1](https://arxiv.org/abs/2609.15692)，首次09-14。摘要是流程图后缀的度量学习与潜在检索，不是连续潜在推理推荐。
- [Safety as a Constraint，2609.13657v1](https://arxiv.org/abs/2609.13657)，首次09-12。摘要中的GRPO用于已推荐物品的解释安全与事实性，没有建立解释先于并影响选择，不归核心。
- [LSF-SR，2609.29815v1](https://arxiv.org/abs/2609.29815)，首次09-24；[Hyperbolic RQ-VAE，2609.26342v2](https://arxiv.org/abs/2609.26342)，首次09-22、09-25修订。摘要分别是潜在表示融合和量化几何，latent不等于推理。本轮不扩大为泛生成式推荐清单。

## 覆盖边界

方法条目已核固定正文，版本及资源状态仅代表本次访问。公开代码可访问不等于数据、权重和运行环境全部完备。智能体、基准及已有条目修订已由维护者整合在下方；最终纳入与检查范围见末节。

## 智能体与评测补录

| 工作 | 首次提交（UTC）；核读版本 | 收录依据与证据边界 | 作者资源 |
| --- | --- | --- | --- |
| AgentRecommender | 2026-09-25 11:58:23；[v1 §2–4](https://arxiv.org/html/2609.31166v1) | 推荐网络的主动扩展与最终约束选择，归智能体。默认扩展8次、输出10项，每域抽100用户；主要测覆盖和约束，扩展改变候选支持，不证明同候选推理增益。 | 官方代码未核实 |
| Spotify 对话智能体 | 2026-09-16 14:48:02；[v1 §3–4](https://arxiv.org/html/2609.30297v1) | 通过合成多轮计划、轨迹对照和编码代理改善推荐规划；归智能体。线上对照是新多轮体验与旧会话细化体验，不能将整套产品收益归因单项规划优化。 | 官方代码未核实；浏览索引abs曾404，直接HTTP与固定HTML成功 |
| RecToolBench | 2026-09-25 02:44:07；[v1 §2–4及Limitations](https://arxiv.org/html/2609.30717v1) | 1,288合成任务、三域、四类工具复杂度，归基准。规则检查与轨迹裁判分列，L4无唯一参考流程；调用成功不保证推荐完成，不能外推生产噪声与延迟。 | [官方仓库](https://github.com/ShawnChenn/RecToolBench)有benchmark、MCP服务和评测脚本 |
| SID reproducibility | 2026-09-21 11:26:49；[v1 §4.1–4.4](https://arxiv.org/html/2609.24430v1) | 归评测研究，为SID推理提供编码对照。全局70:13:17时间切分；warm-only多目标；RQ1保留各方法推断，RQ2–4固定TIGER，去历史物品后热门补足K。不能称所有主表是同解码比较，也不单独证明推理有效。 | [官方SID-Repro](https://github.com/layingfish/SID-Repro)有配置、pipeline、实验和结果目录 |
| Whom Do AI Agents Work For? | 2026-09-16 01:21:56；[v1 Study 1、Measures、Reasoning effort、Limitations](https://arxiv.org/html/2609.17989v1) | 归评测研究。四酒店候选，角色委派×赞助披露，每格500次；比较高低思考深度及生成文本。作者报告角色效应；文字轨迹评分不等于内部机制，受控酒店结论不直接代表真实广告。 | 官方代码未核实 |
| PRAGMA | 2026-09-09 03:31:47；[v2 §3–5](https://arxiv.org/html/2609.09664v2) | 归基准。100合成用户、400查询，兴趣/事件与错误前提；检索证据与建议裁判分开。oracle-session和oracle-summary信息形式不同；不以oracle差异宣称内部因果机制。09-23修订涉及表5 RAG结果，不重复计数。 | [官方代码](https://github.com/yuhyojeong/PRAGMA)有pipeline/metrics；[数据](https://huggingface.co/datasets/stellahj/PRAGMA)实际列出full_sessions、metadata、query_data、response_metrics等JSON |
| Housing compliance / optimization | 2026-09-09 21:51:15；[v1 PDF摘要、§1及§1.1](https://arxiv.org/pdf/2609.10856v1) | 归评测研究。合成租客请求与真实房源的固定候选审计；区分硬约束与相对可行候选的严格支配。支配率依赖候选池组成，非部署产品审计、非CoT消融；不外推真实租户福利。 | HTML不可用；代码发布为作者陈述，归属与可访问入口未核实 |

## 已有条目修订及资源复查

- 批量查询README中101个唯一arXiv ID，全部返回元数据；上次完整截止之后未发现这些条目的新修订。另3篇非arXiv条目不在该批检查内。原始记录保存在本地 `literature/WEEKLY_REVISIONS_20260928.json`。
- 重叠窗口补读 [LIGE-GR v2 §5.2–5.3](https://arxiv.org/html/2609.18148v2)，修订时间09-20 18:06:34。明确候选池约百量级、输出约十量级；b1与b6比较中，纯beam扩展和同时改ListVM/未来估计的方案分开。三组使用相同item VM权重，但仍不能把全部差异归因beam。约20%额外CF组件资源不是可比端到端延迟。未做逐字版本diff，不声称以上内容全部由v2首次加入。
- HiLaR官方仓库仍仅README；SAPO、Re2A的既知地址本次GitHub接口仍404；CogRec结构路由仓库有训练/模型代码，状态未变。不可访问不等于永久未发布。

## 其他边界决定

- [AgentX-Model](https://arxiv.org/abs/2609.30001)、[AURA](https://arxiv.org/abs/2609.16625)、[Auto-RecSys](https://arxiv.org/abs/2609.10922)：核一手摘要，主要为推荐模型开发、日志诊断或自动科研，不是面向用户的推荐决策规划，本轮不纳核心。
- [Recommendation World Models](https://arxiv.org/html/2609.30711v1)：核§3.1–3.2及附录D：围绕冻结排序器的有限候选列表进行一步后果预测和约束选择，P=1的预测深度与H=10的交互长度分开。尚未建立与本库多步推理或搜索机制的直接对应，保留为长期决策近邻，不仅因world model名称纳入核心。
- [ReAdapt](https://arxiv.org/abs/2609.25284)的合成社会关系环境、[From Prompt to Recommendation](https://arxiv.org/abs/2609.23162)的品牌AI搜索观察，未建立与本仓库偏好推理机制的直接关联，本轮不纳入。

## 本轮结果及验证范围

新增10篇：5核心、2基准、3评测研究。清单由104变为114篇（84核心、8基准、11评测、2综述、9背景），17篇精选卡片不变。同步首页、基准选型与来源台账；修正首页旧的评测研究分项计数。

验证覆盖标题/arXiv去重、分类计数、月份排序、文件及锚点、`git diff --check`，并按仓库原配置执行在线链接检查，额外检查本周笔记。发布提交与Actions结果保留在Git历史和本地周检状态；不将尚未完成的检查写成通过。全文核读和仓库浏览均不构成实验复现。
