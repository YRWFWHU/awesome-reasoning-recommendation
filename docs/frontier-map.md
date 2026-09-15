# 前沿研究地图

[返回首页](../README.md) · [方法对照](method-matrix.md) · [基准与资源](benchmarks.md) · [检索记录](../notes/frontier-search-2026-09-15.md)

**观察截止：2026-09-15。** 本页把已收录工作连接为研究问题：哪些机制已有证据，哪些差异仍需要控制实验。下面的最小实验是维护者建议，不是作者已验证的结论，也不构成对选题新颖性的保证。

## 先分清三个目标

| 目标 | 应测量什么 | 不能用什么替代 |
| --- | --- | --- |
| 推荐决策更好 | 排名、约束满足、交互成功或用户结果 | 只看解释更流畅 |
| 推理过程更可靠 | 证据支持、干预后的决策变化、步骤验证 | 只看最终命中目标 |
| 计算使用更有效 | 在明确预算下的效果，或相同效果所需成本 | 只比较各方法的最大模型或最高预算 |

[Descriptive Reasoning Disconnect](https://arxiv.org/abs/2608.23154) 在其控制实验中观察到轨迹质量与离线推荐效果分离；[SelfDR](https://arxiv.org/abs/2609.03313) 则把推理教师的输出用于直接推荐学生。它们提示应分别研究“如何获得推理监督”和“预测时是否需要执行推理”。

<a id="causal-utility"></a>
## 1. 推理到底贡献了什么

**已有入口：** [OneReason](../README.md#paper-onereason)、[Disconnect](../README.md#paper-disconnect)、[SelfDR](../README.md#paper-selfdr)。

这些工作分别提供训练预算对照、表示与推理的控制实验、以及推理自蒸馏视角。系统整体涨分，仍可能来自额外数据、语义对齐或更强教师。

**建议的最小实验：** 固定基座、切分与候选，比较直接训练、CoT 训练但直接预测、CoT 训练并输出推理；再分别控制训练 token 和预测预算。对可显式操作的轨迹加入删除、错配、打乱与等长无关文本干预。

**判定重点：** 分别报告训练收益、执行推理的增量与干预敏感性。测试时替换轨迹可能引入分布偏移，不能只凭一次删除实验宣布发现或否定因果机制。

<a id="item-interface"></a>
## 2. 物品表示如何支撑有效推理

**已有入口：** [TIGER](../README.md#paper-tiger)、[OneRec-Think](../README.md#paper-onerec-think)、[SIDReasoner](../README.md#paper-sidreasoner)、[GREAM](../README.md#paper-gream)。

需要分清三种空间：目录中的真实物品、离散 SID、自然语言描述。SID 前缀命中、最终物品命中和解释语义合理性并非同一个目标。

**建议的最小实验：** 在相同数据上比较标题、SID、SID 加文本对齐；固定解码与候选解析规则，另外报告 SID 碰撞、非法输出和解析失败。加入新物品或物品描述变化后的测试。

**判定重点：** 对齐训练的成本是否带来决策收益；改善是否依赖更容易的输出解析，而非偏好理解。表示层结论需要回到 item-level 指标核对。

<a id="credit-assignment"></a>
## 3. 奖励应该给最终结果，还是给过程

**已有入口：** [GR2](../README.md#paper-gr2)、[SAPO](../README.md#paper-sapo)、[ReRec](../README.md#paper-rerec)、[PROMISE](../README.md#paper-promise)。

这里存在不同路线：结果奖励优化整段轨迹、按步骤分配信用，以及训练过程验证器来引导搜索。过程奖励模型的训练不必是 RL；不能仅按标题里的 reward 归类。

**建议的最小实验：** 固定策略模型与 rollout 预算，对照最终奖励、步骤奖励及混合奖励；独立更换验证器，加入候选顺序打乱、重复物品、格式正确但无实际改进等压力测试。

**判定重点：** 在训练奖励之外报告推荐效果与验证器泛化；奖励提升而外部指标停滞时，检查捷径和评估器偏置。

<a id="adaptive-compute"></a>
## 4. 谁需要更多推理，何时应该停止

**已有入口：** [ReaRec](../README.md#paper-rearec)、[EGLR](../README.md#paper-eglr)、[ManCAR](../README.md#paper-mancar)、[Where Reasoning Matters](../README.md#paper-where-reasoning-matters)。

潜在迭代、额外文本 token、候选验证和树搜索消耗的是不同计算。平均步数少，也不必然意味着尾部延迟低。

**建议的最小实验：** 在同一服务配置下扫预算，比较固定步数、随机分配、启发式提前停止和学习式分配；按历史长度、冷启动程度及请求难度分组。阈值仅用验证集选择。

**判定重点：** 同时报告效果、总计算、平均延迟与 p95。识别在这些维度上不被其他配置同时超越的方案；不要把可访问测试答案的事后步数选择当作可部署策略。

<a id="internalization"></a>
## 5. 怎样保留收益并减少在线推理

**已有入口：** [WhisperRec](../README.md#paper-whisperrec)、[LaRec](../README.md#paper-larec)、[rEDMRec](../README.md#paper-redmrec)、[SelfDR](../README.md#paper-selfdr)、[STAR](../README.md#paper-star)。

需要区分潜在 token 压缩、参数蒸馏、外部记忆，以及把多智能体过程压进单模型。这些路径的更新方式和部署成本不同。

**建议的最小实验：** 对照显式教师、直接学生、蒸馏学生和记忆检索学生，统一数据与候选；将离线轨迹生成、训练/建库、记忆更新和在线预测分别计时。再加入兴趣漂移或新物品测试。

**判定重点：** 成本被减少了，还是移动到了离线阶段？训练时带答案的教师监督需要单独记录，但这本身不等于测试泄漏；必须检查测试输入与跨切分资源是否隔离。

<a id="interaction"></a>
## 6. 从静态推荐转向有目标的交互

**已有入口：** [MGFRec](../README.md#paper-mgfrec)、[AgentDR](../README.md#paper-agentdr)、[HARPO](../README.md#paper-harpo)、[NEXT](../README.md#paper-next)、[Agentic Roadmap](../README.md#paper-agentic-roadmap)。

对话澄清、工具调用和目录检索使推理能接触外部证据，但也引入轮数、工具可用性与模拟用户的影响。

**建议的最小实验：** 固定工具和总调用预算，比较单轮推荐、固定工作流、动态规划；更换用户模拟器并保留独立真人或真实日志评估。测试约束延迟揭示、反馈冲突和工具失败。

**判定重点：** 轨迹成功率、约束满足、无效调用与交互成本一起报告。模拟器中更会“讨好用户”不能直接等同于真实用户收益。

<a id="evaluation"></a>
## 7. 让评测识别推理的收益与失败

**已有入口：** [τ-Rec](../README.md#paper-tau-rec)、[RPCBench](../README.md#paper-rpcbench)、[RecIF-Bench](../README.md#paper-openonerec)、[CRS 协议研究](../README.md#paper-crs-protocol)。

固定负例排序、全库检索、多轮约束验证、错误前提诊断衡量不同能力。相同指标名不保证同一实验难度。

**建议的最小实验：** 固定候选检索器，分别改变评分、解码与反馈；单独报告候选召回、条件重排和完整系统结果。对 LLM 评审做跨模型家族抽查，并验证提示、顺序和输出长度敏感性。

**判定重点：** 流程贡献是否被模型名称遮住；推理文本评分是否与决策评分相互污染。可靠性 `pass^k` 与多次尝试的 `pass@k` 必须分别定义。

<a id="generalization"></a>
## 8. 跨领域、跨模态与变化中的用户

**已有入口：** [MusiCRS](../README.md#paper-musicrs)、[Conv-FinRe](../README.md#paper-conv-finre)、[ReasonRec](../README.md#paper-reasonrec)、[IntuRec](../README.md#paper-inturec)。

多领域或多模态输入不自动证明统一推理能力；一种模态可能被忽略，跨域提升也可能依赖共享物品或教师背景知识。

**建议的最小实验：** 留出领域、时间段或物品，做单模态消融与模态冲突测试；区分适配训练、零样本迁移和在线更新。对记忆方法检验陈旧偏好的更新与移除。

**判定重点：** 泛化收益、约束错误和成本能否同时保持；领域专用任务的成功不直接外推到通用推荐。

## 如何选一个可执行的研究起点

| 可用条件 | 先做什么 | 有说服力的产物 |
| --- | --- | --- |
| 已有离线推荐代码与数据 | 推理有无、预算控制和候选协议对照 | 可复现的效果—成本曲线及消融 |
| 有可训练的推荐 LLM | 奖励分配或推理蒸馏 | 同基座、同数据下的增量证据 |
| 只有 API 与目录工具 | 固定预算的规划/交互实验 | 可执行轨迹、约束验证和调用成本 |
| 有真实用户或日志 | 模拟器校准、长期偏好与反馈验证 | 离线到真实交互的差异分析 |

判断进展时，优先问“排除了哪些替代解释、公开了哪些复现条件”，再看单个最优分数。实验记录模板见 [评测指南](evaluation.md)。
