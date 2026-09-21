# 方法与证据对照

[返回首页](../README.md) · [前沿地图](frontier-map.md) · [证据卡片](frontier-reading.md) · [基准选型](benchmarks.md)

**核实日期：原表2026-09-15；本周补充2026-09-21。** 对照 39 个代表方法，重点是推理对象、学习信号和计算发生位置。各论文的数据、候选、骨干与预算不同，本表不构造跨协议 SOTA 排行榜。未核实的字段保留未知，不根据方法名补猜。

## 读表方法

- **摘要级**：已核标题、日期与作者摘要；不足以判断完整消融和成本。
- **局部正文级**：已读具体方法、实验或成本章节，不表示全文审稿。
- **官方代码**：只表示作者来源可追溯且页面可读；占位页单独注明，所有方法均未由本仓库复现。
- **计算位置**：显式 token、潜在步数、检索次数、候选量和训练 FLOPs 分别计数。更多训练数据不等于更多测试时计算。

## 显式推理、奖励与预算控制（9）

| 方法 | 任务 | 推理表示 | 训练信号 | 推理计算方式 | 已核实证据 | 代码状态 |
| --- | --- | --- | --- | --- | --- | --- |
| [ReRec](../README.md#paper-rerec) | 复杂查询推荐助手 | 文本推理片段 | 排名＋查询/偏好对齐奖励；片段优势；训练课程 | 多步文本分析 | 摘要；方法结构 | 作者摘要直链，仓库可读 |
| [SIDReasoner](../README.md#paper-sidreasoner) | 下一物品预测 | 文本推理＋SID | 多任务对齐、轻量激活、结果驱动 GRPO；前缀/格式奖励 | 推理后生成 SID | 局部 §3.3；源码首页明确三阶段 | 作者全文直链，仓库可读 |
| [ManCAR](../README.md#paper-mancar) | 序列推荐 | 潜在状态与物品分布 | 目标预测＋图先验 KL 约束 | 分布收敛提前停止 | 局部 §2.6、§3.3、§3.6；不是等预算对比 | 作者摘要直链，仓库可读 |
| [R2Rank](../README.md#paper-r2rank) | 候选集排名 | 每候选文本推理＋评分头 | 自检 SFT；列表 NDCG；PPO/REINFORCE | 每候选独立推理后排序 | 局部 §3.3、§4.1、§4.3；固定 20 候选 | 未核实 |
| [EGLR](../README.md#paper-eglr) | 生成式重排 | 候选加权聚合的潜在 token | 预训练 evaluator 评分＋GRPO | 熵门控、每物品推理上限；多列表选择 | 局部 Algorithm 1、§5.6–5.7；收益递减 | 未核实 |
| [DTRec](../README.md#paper-dtrec) | 序列推荐 | 潜在状态 | 原型过程监督＋软停止训练 | 三信号 MLP 停止概率，阈值提前退出 | 局部 §3.1–3.2；未精读预算实验 | 未核实 |
| [GREAM](../README.md#paper-gream) | 生成式推荐 | 文本 CoT＋离散物品索引 | 合成轨迹 SFT；前缀奖励＋成功奖励 SRPO | direct/reason 双模式 | 局部 §5、§6.3；不同模式不同指标 | 作者全文直链，仓库可读 |
| [RecLLM-R1](../README.md#paper-recllm-r1) | 推荐列表 | 文本 CoT＋物品文本 | SFT＋GRPO 多目标奖励 | 多步文本决策 | 一手摘要；未核实等预算效果 | 未核实 |
| [R²ec](../README.md#paper-r2ec) | 下一物品推荐 | 文本链＋独立推荐头 | RecPO 融合奖励 | 链生成后推荐头物品预测 | 一手摘要；未精读预算对照 | 作者摘要直链，仓库可读 |

来源：[RL / TTS 逐篇版本与证据](../notes/frontier-rl-tts-2026-09-15.md)。

## 潜在推理、预算分配与蒸馏（8）

| 方法 | 任务 | 推理表示 | 训练信号 | 推理期预算 | 已核实证据 | 代码状态 |
| --- | --- | --- | --- | --- | --- | --- |
| [LatentR³](../README.md#paper-latent-r3) | LLM 推荐 | 连续潜在 token | SFT → 改进 GRPO；规则与连续奖励；无 CoT 轨迹监督 | 少量潜在 token；具体默认值未核实 | 摘要：训练框架与多基线集成；未核成本章节 | 作者摘要直链；源码可见 |
| [FLR](../README.md#paper-flr) | 序列推荐 | 多因子注意力细化潜在思考 | 预测监督、正交/多样性/稀疏正则、GRPO | 成本实验默认额外 1 个潜在 token；因子数另计 | 方法、因子/奖励消融、成本；显式 CoT 对照 beam 不同 | 作者正文直链；源码可见 |
| [IntuRec](../README.md#paper-inturec) | LLM 推荐 | 候选先验初始化的连续轨迹 | 本轮未核实完整损失 | top-K 候选提取 + 后续潜在推理；K 与默认步数未核实 | 摘要与源码目录；未核因果或成本对照 | 作者摘要直链；源码可见 |
| [IBA](../README.md#paper-where-reasoning-matters) | 语义 ID 下一物品预测 | 各 SID 位置的隐藏状态细化 | 两阶段 CE；预测增益监督与 lookahead loss | 默认总 B=6；先验 (3,2,1,0)，每用户分配一次；beam20 | 方法、预算与实现；有固定/非匹配分配对照 | 未核实 |
| [LaRec](../README.md#paper-larec) | 生成式下一物品推荐 | 与教师对齐的连续潜在轨迹 | 步骤/方向对齐、个性化采样与 RL | 成本实验 K=6；受约束 beam；单 H20 | 多组件消融、K 扫描、逐数据集时延；线上另用离线表征召回 | 未核实 |
| [HiLaR](../README.md#paper-hilar) | 生成物品标题的推荐 | 从长期到当前意图的层次潜在状态 | 偏好层次对齐 + 最终反馈 + 层级过程奖励 | K 可配置；CDs 敏感性中 K=4 较好，非全数据默认声明 | 方法摘要；过程奖励对照与参数敏感性 | 官方仓库仅 README / Coming Soon |
| [EvoReason](../README.md#paper-evoreason) | 语义 ID 生成推荐 | 教师推理原语 → 学生潜在 token | 置信门控在策略蒸馏、KV 对齐、结果 RL | 在线 M 个潜在 token；原语库默认 K=5 不等于 M；beam10 | 原语/OPD/自演化消融；附录成本 | 未核实；正文依赖仓库不能充作本作代码 |
| [rEDMRec](../README.md#paper-redmrec) | 20 物品候选排序 | 四通道外部经验记忆 | 教师提取、按排序奖励修改记忆；学生冻结 | 默认每通道 top-5；记忆更新另有多代理/轮次成本 | 通道消融、无辩论改写控制、代理数量成本；非全库检索评估 | 未核实 |

来源：[潜在推理逐篇版本与证据](../notes/frontier-cot-latent-2026-09-15.md)。

## 交互、工具与多智能体内化（4）

| 工作 | 推理对象与形式 | 训练信号 | 推理发生位置 | 已核验的评测范围 | 成本或关键限制 |
| --- | --- | --- | --- | --- | --- |
| [STAR](../README.md#paper-star) | 协同证据、规划、工具、反思轨迹 | 筛选轨迹 SFT + GRPO | 单智能体生成与工具 | AgentRecBench；20 候选；HR@1/3/5 平均 | 89 s 对教师 461 s；非亚秒级 |
| [HARPO](../README.md#paper-harpo) | 会话偏好、价值网络引导推理树、抽象工具操作 | 分层偏好优化与多阶段训练 | 对话轮次中的搜索 | ReDial/INSPIRED/MUSE；100 候选 | 每轮 298 ms 对无搜索 88 ms；MUSE 用文字代理 |
| [AgenticRec](../README.md#paper-agenticrec) | Think–Act–Observation；难候选双向比较 | GRPO + 排序难例反馈 | 在线工具推理循环 | Amazon 四子域；20 候选；HR/NDCG | 单 A800 平均每请求 16.233–20.678 s；最多 10 次工具交互 |
| [NEXT](../README.md#paper-next) | 视频证据 → 下一意图 → 候选验证 | 感知 RL、SFT、GRPO | 离线/近线关系挖掘，线上关系召回 | 1,000 视频的 LLM judge + 线上 A/B | 作者报告 watch time +0.53%；未隔离各阶段因果贡献；全库挖掘仍昂贵 |

来源：[智能体逐篇版本与证据](../notes/frontier-agents-eval-2026-09-15.md)。协议研究另见 [基准选型](benchmarks.md)。

## 直接预测自蒸馏（1）

| 方法 | 任务与表示 | 训练信号 | 预测期计算 | 已核实证据与限制 |
| --- | --- | --- | --- | --- |
| [SelfDR](../README.md#paper-selfdr) | 理由教师 → 候选推荐学生 | GRPO 推理器、动态软目标自蒸馏 | 学生直接预测；不在线输出教师长链 | §3、§4.4–4.5；特定候选协议和硬件；离线训练成本增加；[证据卡](frontier-reading.md#selfdr) |

## 基础路线对照（6）

| 方法 | 推理对象与表示 | 学习信号 | 计算位置 | 已核实证据与限制 |
| --- | --- | --- | --- | --- |
| [OneRec-Think](../README.md#paper-onerec-think) | 文本推理接入物品语义 ID | 对齐、轨迹 SFT、GRPO | 离线推理与在线生成分工 | [方法与预算卡片](reading-notes.md#onerec-think)；不能混淆两阶段成本 |
| [OneReason](../README.md#paper-onereason) | 语义感知与三层文本推理 | 分阶段 SFT 与 RL | 训练/预测 thinking 分开对照 | [实验卡片](reading-notes.md#onereason)；具体收益依赖训练和领域 |
| [GR2](../README.md#paper-gr2) | CoT 后生成重排列表 | 教师轨迹、DAPO、条件奖励 | 在线候选重排 | [奖励卡片](reading-notes.md#gr2)；检查照抄候选顺序的奖励捷径 |
| [ReaRec](../README.md#paper-rearec) | 序列末端隐藏状态迭代 | 多步表示学习；细节见原文 | 预测时潜在迭代 | 摘要与资源核实；摘要事后上限不等于部署平均收益 |
| [PROMISE](../README.md#paper-promise) | 层级 SID 中间路径 | 过程奖励模型 | 搜索与验证 | 摘要核实；并非自然语言 CoT；不默认标为 RL 训练 |
| [TTR](../README.md#paper-ttr) | 多模态对话意图与候选匹配 | 生成检索与验证器 | 增加候选验证计算 | [方法卡片](reading-notes.md#ttr)；验证预算和初始候选需一起记录 |

基础来源：[来源索引](sources.md)；本轮新方法的代码状态以各来源笔记记录为准。

## 如何做出可比的实验

先固定任务、数据切分、候选与可见证据，再分别对齐训练预算和预测预算。尤其要避免：

1. 用 20 候选排序与全库生成的 NDCG 直接排名。
2. 用潜在 token 数与文字 token 数当作等量 FLOPs。
3. 把训练期间组件重训消融解释为同一模型的测试时推理贡献。
4. 只计在线生成，忽略教师轨迹、记忆更新、离线检索和模型训练。
5. 把同名 Pass@K、pass^k 或不同任务的平均分当作同一指标。

可复用的记录字段与控制实验见 [评测指南](evaluation.md) 和 [前沿研究地图](frontier-map.md)。

## SID 与潜在推理的直接交叉（4）

| 方法 | 计算或表示 | 监督与推理流程 | 必须区分的概念 | 核实范围 |
| --- | --- | --- | --- | --- |
| [S²GR](../README.md#paper-s2gr) | 每个 SID 前的潜在 thinking token | 码本层次语义对比监督、协同与均衡码本 | 中间语义对齐不是干预意义上的因果验证 | [v3](https://arxiv.org/html/2601.18664v3)：摘要、引言与方法描述 |
| [LASAR](../README.md#paper-lasar) | 循环隐状态反馈、每样本深度 | SID grounding → CoT 锚点双向 KL → GRPO/REINFORCE | 循环前向、离线教师成本与线上 beam 成本分别计算 | [v2](https://arxiv.org/html/2605.10207v2)：引言、结论与相关工作 |
| [PauseRec](../README.md#paper-pauserec) | 预置 pause token 的计算位置 | 先仅训 pause 嵌入，再用目标 SID 损失微调 | 固定 pause 位置不等同于逐步反馈前一隐状态 | [v2](https://arxiv.org/html/2606.14142v2)：§5、§6.3–6.4 |
| [Latte](../README.md#paper-latte) | 离散 latent token 条件化多棵 SID 树 | 随机 latent 前缀训练，多路径聚合；另探索排列绑定 | 属于必要背景；离散路径变量不是连续推理步 | [v1](https://arxiv.org/html/2605.06331v1)：摘要、引言与多树/排列描述 |

来源：[本次29篇补录与核读范围](../notes/latent-sid-search-2026-09-15.md)。

## 2026-09-21 补充：计算位置与证据边界（7）

| 方法 | 推理影响决策的位置 | 训练与预测的区别 | 固定版本证据 |
| --- | --- | --- | --- |
| [Re2A](../README.md#paper-re2a) | 场景偏好状态引导回复和物品选择 | GRPO整轨迹rubric评分；再做偏好条件DPO | [v1 §3](https://arxiv.org/html/2609.18249v1)；代码入口404 |
| [NarraLite](../README.md#paper-narralite) | 潜在叙事token引导SID续集生成 | 训练用目标语义对齐；预测无教师，潜在token并行 | [v1 §4–6](https://arxiv.org/html/2609.16070v1)；非个性化任务，消融并非逐指标一致下降 |
| [P³Rec](../README.md#paper-p3rec) | 先验/后验偏好知识进入检索表示 | 后验只训练使用；预测仍编码先验偏好 | [v3 §3.5.2](https://arxiv.org/html/2609.13993v3)；离线LLM成本另计 |
| [Trade-Up蒸馏](../README.md#paper-trade-up) | 理由监督商品对关系分类 | 在线无文字生成；按商品类型进行有标签适配 | [v1 §2–4](https://arxiv.org/html/2609.05363v1)；不等同逐请求无监督TTT |
| [LIGE-GR](../README.md#paper-lige-gr) | 未来价值引导列表前缀搜索 | 闭式未来估计，非另训价值网络；b=1/6需区分 | [v1 §3.3、§5.3](https://arxiv.org/html/2609.18148v1)；b=6端到端时延未给出 |
| [AtomRec](../README.md#paper-atomrec) | 语义链接、多跳证据合成后排序 | 记忆维护及在线证据合成都有成本 | [v1 §2.4–2.6](https://arxiv.org/html/2609.04882v1)；默认10候选，不证明路径忠实性 |
| [TGR](../README.md#paper-tgr) | 离线完整SID reason tokens注入生成器 | 首级SID深度监督；K=0离线导出；无请求rollout | [v1 §5.2.2、§5.5](https://arxiv.org/html/2609.00986v1)；表16不含GMR |

除已另述的资源外，以上新增方法官方实现未核实。未记录的训练预算、候选总量或绝对成本均为未知。详见[周检来源与限定](../notes/weekly-search-2026-09-21.md)。
