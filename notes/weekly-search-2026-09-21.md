# 2026-09-21 每周文献检查

[返回首页](../README.md) · [来源总表](../docs/sources.md)

## 窗口与方法

- 首轮接续基准：2026-09-15；向前重叠14天，检索窗口为 **2026-09-01 至 2026-09-21 01:10 UTC（北京时间09:10）**。
- 基线：`69cb544baf2e1ed8bccaa5ffb36d6e7648f467ff`；检查工作树并 fetch 后本地与 origin/main 一致。保留原有未跟踪 AGENTS.md。
- 使用 research 技能，由后台研究代理与维护者分工核实。查询 recommendation/recommender 与 reasoning、latent、chain-of-thought、reward、agentic、distillation、benchmark、test-time scaling、adaptive 的组合，并使用月份、日期范围与 arXiv ID 检索。
- [外部生成式推荐列表](https://hafred.github.io/awesome-generative-recsys/)仅用于发现线索。收录依据为下表一手摘要、首次提交记录和固定版本正文；不采用其他列表的评分、资源状态或录用推断。
- 新增 **7篇：6篇核心方法、1篇评测研究**；更新已有 TGR 的监督与部署边界。总97篇（74核心、6基准、7评测、1综述、9背景）。随附基准不重复计篇；P³Rec 的 v1/v2/v3 合为一条。
- 本轮是文献核读与资源检查，没有运行论文实验，不构成复现。搜索索引可能有延迟，不能宣称无遗漏；下轮继续重叠检索。

## 新增条目的一手证据

| 工作 | 首次提交（UTC） | 固定版本及核读位置 | 分类与证据边界 |
| --- | --- | --- | --- |
| Re2A | 2026-09-16 | [v1](https://arxiv.org/html/2609.18249v1)，§3–4；[提交记录](https://arxiv.org/abs/2609.18249) | 智能体/情境对话推荐；rubric 评估整条 thought/state。SIMMC 2.1、SCREEN，不是全库序列推荐。 |
| NarraLite | 2026-09-13 | [v1](https://arxiv.org/html/2609.16070v1)，§3–6；[提交记录](https://arxiv.org/abs/2609.16070) | 潜在推理；无用户的短剧续集任务。默认30视觉token、2潜在token、trie解码10候选；实验环境8张H20。 |
| P³Rec | 2026-09-12 | [v3](https://arxiv.org/html/2609.13993v3)，§3、§3.5.2、§4.6；[提交记录](https://arxiv.org/abs/2609.13993) | 蒸馏；后验只在训练使用。当前v3修订于09-16，不据此改变首次日期。 |
| LIGE-GR | 2026-09-16 | [v1](https://arxiv.org/html/2609.18148v1)，§3.3、§4、§5.3、附录A；[提交记录](https://arxiv.org/abs/2609.18148) | 结构化搜索；以未来价值估计决定保留哪些列表前缀，区别于仅按生成概率扩beam。 |
| Distill Globally, Adapt Locally | 2026-09-04 | [v1](https://arxiv.org/html/2609.05363v1)，§2–4、§6；[提交记录](https://arxiv.org/abs/2609.05363) | 蒸馏；商品升级替代关系分类。支持集与评测集商品对不重叠，但不保证商品或品牌不重叠。 |
| AtomRec | 2026-09-04 | [v1](https://arxiv.org/html/2609.04882v1)，§2.4–2.6、§3、§4.6、附录D；[提交记录](https://arxiv.org/abs/2609.04882) | 智能体；多跳记忆证据参与排序，默认10候选、附录20候选，不是全库检索。 |
| Transparent UPR 复现研究 | 2026-09-17 | [v1](https://arxiv.org/html/2609.19831v1)，§5.4.2–5.4.3；[提交记录](https://arxiv.org/abs/2609.19831) | 评测研究；文本编辑可有少量名次波动，不能把摘要概括扩大成所有排序严格不变。 |

### 核读后的重要限定

- **NarraLite：** 作者正文概括两项消融均下降，但表2 Eval H@1 中完整模型0.1988，去掉LNR为0.2028；因此不写“所有指标一致提升”。§6.3的消融名称与表2也不完全一致。上述是维护者对[v1表2与§6.3](https://arxiv.org/html/2609.16070v1)的核对，不是复现结论；不抄未完整给定统计口径的吞吐优势。
- **LIGE-GR：** §5.3分别比较更宽beam和同时改变价值目标/未来估计的配置，不能把后一配置全部收益归给beam。作者对b=6报告资源估计而非可比端到端延迟，训练成本也不能由该数反推。[v1 §4、§5.3与附录A](https://arxiv.org/html/2609.18148v1)
- **TGR（已收录）：** §5.2.2的PRL是首级SID交叉熵深度监督，不是推理步骤语义正确性标签。表16排除GMR；线上无rollout不代表训练、离线刷新和注入都没有成本。[v1 §5.2.2、§5.5](https://arxiv.org/html/2609.00986v1)
- **UPR：** 本文作者做了复现，本仓库只核读。负面发现针对评分回归/测试集重排协议，不能升级为所有偏好画像或思维链无效。[v1 §5.4](https://arxiv.org/html/2609.19831v1)

## 资源与版本

- UPR正文脚注直链的[作者仓库](https://github.com/nmamie/transparent_user_profiles)可访问，有训练、评估与干预脚本；未运行代码。
- Re2A作者入口 `https://github.com/DongdingLin/Re2A` 网页与API返回404，保留地址追踪，首页标未核实；其余新增方法的官方实现未核实。
- [HiLaR作者仓库](https://github.com/hupeiyu21/HiLaR)本轮API列表仍仅README。SAPO作者入口 `https://github.com/zhengzaiyi/SAPO` 仍返回404。没有据此推断永久未开源。
- 对已有CoT、RL、蒸馏、智能体及评测类48个arXiv页面和潜在/TTS/背景类39个页面核对版本史；未发现这些已检查条目在窗口内新增修订。[IntuRec](https://arxiv.org/abs/2606.27684)仍显示六月v1，不采用镜像的九月修订说法。未使用arXiv的工作不包含在这个版本史统计内。
- 会议Comments不单独充当录用证据，新增条目仅标arXiv。未核实的预测候选总量、训练预算和绝对成本保留未知。

## 暂缓及范围外

- **SARA：** [v1 §2.3、§5](https://arxiv.org/html/2609.17639v1)的正负理由作为排名特征，尚不足以明确归入多步推理/轨迹蒸馏；放[待核清单](pending-papers.md)，不计核心。
- **Recommendation Retrievers Need Verifiers：** [作者摘要](https://arxiv.org/abs/2609.12270)是以物品标识符似然评分做后置重排，暂未建立推理步骤/搜索机制，不因verifier一词收录核心。
- **LION / Self-Evolving Memory：** [摘要](https://arxiv.org/abs/2609.15598)的稀疏记忆/持续适应不足以单独证明推理机制，暂不纳核心。
- **AGAS：** [论文](https://arxiv.org/abs/2609.09551)研究攻击协作，非本仓库的偏好推荐推理范围。
- **PASS：** [论文](https://arxiv.org/abs/2609.13760)属于科研投稿辅助的相邻线索，未确立与本清单范围的对应，不新增。
- 通用潜在推理和通用文档检索论文不因有latent/reasoning/RL字样自动进入推荐核心；窄查询空结果不当作“没有新论文”的证据。
