# 潜在推理与 SID 交叉：文献补录

核实日期：2026-09-15。先查本仓库原有52条，再查询一手论文。新增29条后总81条：62核心、6基准、6评测研究、1综述、6背景。未开展实验复现。

|条目|首次提交/日期口径|实际核读|收录理由与资源|
|---|---|---|---|
|[S²GR](https://arxiv.org/abs/2601.18664)|2026-01-26|v3摘要、引言、方法描述|每SID前潜在思考及码本过程监督；代码未核实|
|[LASAR](https://arxiv.org/abs/2605.10207)|2026-05-11|v1/v2摘要、引言，v2结论及相关工作|循环latent、CoT锚点、自适应深度；同名CVPR导航项目不是本论文，未混用代码|
|[Latte](https://arxiv.org/abs/2605.06331)|2026-05-07|v1摘要、引言；多树、排列说明|背景；离散latent变量不等同连续推理；作者[实现](https://github.com/hyp1231/Latte)已打开核对|
|[BARGE](https://arxiv.org/abs/2607.21028)|2026-07-23|v1摘要、引言；v3摘要、相关工作入口|层级路径重排与双通道搜索；核心结构化搜索；v3直连HTTP406，网页工具可读|
|[Why Thinking Hurts](https://arxiv.org/abs/2602.16587)|2026-02-18|v1摘要、引言|显式CoT漂移诊断与训练免除的解码校正；代码未核实|
|[TGR](https://arxiv.org/abs/2609.00986)|2026-09-01|v1摘要、引言、系统对照|TGR-Reason离线latent训练和reason tokens；不是在线多步rollout；代码未核实|
|[Intent-Driven SID](https://arxiv.org/abs/2605.07613)|2026-05-08|v1摘要、引言；[ACL正文](https://aclanthology.org/2026.acl-industry.130.pdf)定位|意图推理、SID前缀与实时新闻池匹配；代码未核实|
|[PauseRec](https://arxiv.org/abs/2606.14142)|2026-06-12|v2摘要、方法§5、消融§6.3、相关工作入口|pause预训练+SID监督；额外计算与循环反馈需区分；代码未核实|
|[TwiSTAR](https://arxiv.org/abs/2605.11553)|2026-05-12|v1摘要、引言、相关工作、结论|规划器选择检索/重排/显式推理；代码未核实|
|[LIME-Rec](https://arxiv.org/abs/2608.01260)|2026-08-02|v1摘要、引言、相关工作、结论|语义收益归因审计，单列评测研究；作者[实现](https://github.com/Double-wk/LIME-Rec)已核对|
|[CoderRec](https://ojs.aaai.org/index.php/AAAI/article/view/38680)|2026-03-14正式出版|AAAI官方摘要/出版记录；作者PDF入口|下游潜在思考与跨规模SID协作；未找到可核实arXiv首次日期，首页明确使用正式出版日期，不推断最早预印本时间|

## 范围与解释

- 上述均按去版本arXiv ID或DOI/标题去重。TGR总报告与BARGE独立论文为不同记录；不把TGR的每个系统模块各算一篇。
- SID树结构、额外计算与推荐效果的联系需要受控实验。Latte理论结论依赖文中假设，不可概括成“任何自回归模型都不能表示任意偏好”。
- S²GR和LASAR已涉及中间监督；对齐可视化、attention和probe本身不证明因果忠实性。
- CARD（2604.26427）和HiD-VAE（2508.04618）仅作相邻编码背景线索；TriAlignGR后续核实其§3.4 CoT兴趣实际进入SID构建，已从待核实转为训练期推理条目。没有把所有SID方法自动加入核心。
- 搜索还出现其他awesome中的TwiSTAR、PauseRec线索，随后回到一手论文完成核实。其他awesome不能作为方法结论或优先性依据。

## 逐主张查新追加核实（18条）

所有条目均核对作者摘要页、首次提交记录及正文相关段落；代码未逐一打开，因此统一保留“未核实”。不把匿名投稿、PDF模板或作者自述当作正式录用证据。

|条目|首次提交|分类与核实重点|
|---|---|---|
|[PLR](https://arxiv.org/abs/2601.03153)|2026-01-06|用多个连续推理流探索用户偏好，以多样性正则和混合聚合整合结果；扩展的是推理宽度，而非只增加单条链的深度。|
|[LARES](https://arxiv.org/abs/2505.16865)|2025-05-22|在每个循环步骤细化全部输入 token，结合轨迹与步骤对齐预训练、强化后训练扩展潜在计算深度。|
|[RecRec](https://arxiv.org/abs/2607.12945)|2026-07-14|将历史压缩为多个兴趣向量，在独立中间空间循环细化，再用于预测；通过深度监督支持调整推理步数，训练不依赖 RL。|
|[DiffuReason](https://arxiv.org/abs/2602.09744)|2026-02-10|先用潜在思考形成意图假设，再通过扩散细化表示，并以 GRPO 联合对齐排名目标。|
|[Latent Cross Reasoning](https://arxiv.org/abs/2508.04152)|2025-08-06|从搜索与推荐历史中形成兴趣表示，再迭代筛取对推荐有用的搜索证据；使用对比学习与强化学习对齐目标物品和排名。|
|[RecGPT-V3](https://arxiv.org/abs/2607.15591)|2026-07-17|以持续更新的用户记忆连接文本标签与 SID，并把显式意图分析压缩为可学习潜在 token；需分别核算记忆维护、训练与在线推理成本。|
|[CaLIR](https://arxiv.org/abs/2606.07075)|2026-06-05|在生成商品 SID 前执行类别引导的连续意图推理，结合多意图训练与查询相关前缀树。实验任务是电商搜索，不能直接视为序列推荐结论。|
|[ISRF](https://arxiv.org/abs/2603.13934)|2026-03-14|以多步属性推理构造物品语义和用户群体兴趣，再通过个体与群体信息的迭代优化改进推荐；应区分语义构建成本与预测成本。|
|[DeepInterestGR](https://arxiv.org/abs/2602.18907)|2026-02-21|通过多模态模型的思维链挖掘兴趣，将兴趣信息写入物品离散编码，并用于监督微调与奖励设计。收录为预印本，未采用正文模板中的会议标注。|
|[RGD](https://arxiv.org/abs/2607.25344)|2026-07-28|在 SID 解码期间用奖励模型调整路径概率，使高价值候选有机会在前缀阶段保留；固定生成器，通过测试时控制改变目标权重。|
|[V-STAR](https://arxiv.org/abs/2602.10699)|2026-02-11|选择有价值的分叉节点投入搜索预算，并利用兄弟分支间的奖励差异学习；研究概率主导解码与奖励目标不一致的问题。|
|[SIDScope](https://arxiv.org/abs/2608.18779)|2026-08-19|诊断物品到 SID 的映射结构、前缀候选暴露、路径到物品的解析及更新后的模型交接。它评估接口风险，不直接证明模型执行了潜在推理。|
|[Faithful SID Evaluation](https://arxiv.org/abs/2605.25330)|2026-05-25|区分命中 SID 与命中具体物品，分析编码碰撞引起的计分偏差，并提供物品级修正和消除碰撞的后处理。当前标题与初版不同，合并为一条。|
|[Temporal Cold SID](https://arxiv.org/abs/2607.21101)|2026-07-23|使用绝对时间划分与前缀探查，区分已有 token 的重组和包含未见 token 的新物品生成；检查冷物品在编码与解码空间中是否可达。|
|[SETRec](https://arxiv.org/abs/2502.10833)|2025-02-15|以无序 token 集合表达物品并并行生成，减弱固定序列依赖；是比较 SID 顺序与潜在推理时的重要编码对照。|
|[HCGRec](https://arxiv.org/abs/2608.11980)|2026-08-12|在训练时对难例提供最短目标前缀提示，分别对提示 token 和采样后缀分配学习信号。属于 SID 奖励学习背景，目标提示不能用于部署评测。|

Faithful SID Evaluation 当前标题为 *Faithful Evaluation of Semantic-ID Tokenizers for Generative Recommendation*，初版检索标题为 *How Reliable Are Semantic-ID Tokenizer Comparisons in Generative Recommendation?*；以 arXiv 2605.25330 合并。DeepInterestGR 初版正文的 KDD 模板时间早于其 arXiv 提交且与所述模型时间不一致，本记录只确认预印本存在与其方法描述，不确认该会议归属或结果。

|追加条目|首次提交|核实说明|
|---|---|---|
|[REG4Rec](https://arxiv.org/abs/2508.15308)|2025-08-21|v4摘要、相关工作；无序MPQ语义路径、奖励与CORP自检；不能自动归为连续潜在推理。|
|[TriAlignGR](https://arxiv.org/abs/2605.05249)|2026-05-05|v1摘要、§3.4 MDIM及§4.2消融；推理产物用于离线SID构建，已完成原待核项。|

## 范围外但与查新相关的来源

这些论文仅保留为相邻机制或实验协议资料，不扩充核心清单：

|来源|范围差别|
|---|---|
|[GenCDR](https://arxiv.org/abs/2511.08006)、[GenCDSR](https://arxiv.org/abs/2607.28659)、[DACT](https://arxiv.org/abs/2603.29705)|跨域编码、串并行生成或持续分词；未据此认定显式/潜在推理机制。|
|[InforID](https://arxiv.org/abs/2608.09685)|分配离线编码槽位与码本容量，不是在线思考预算。|
|[Pulling back information geometry](https://proceedings.mlr.press/v151/arvanitidis22b.html)|概率几何基础，含电影偏好插值；不是SID生成式推理方法。|
|[IIT](https://proceedings.mlr.press/v162/geiger22a.html)、[Causal Abstraction](https://arxiv.org/abs/2301.04709)|状态交换监督、因果抽象的基础来源。|
|[PMPS](https://arxiv.org/abs/2609.09928)、[Emergent Search and Backtracking](https://arxiv.org/abs/2602.08100)、[Parallel Latent TTS](https://aclanthology.org/2026.acl-long.2069/)|通用潜在推理监督、回溯和计算扩展，任务不是推荐。|
|[CoDeR+](https://doi.org/10.1145/3778863)|传统序列推荐的需求混杂与反事实调整；不等同SID隐状态的因果推理监督。|
|[UGR](https://hexiangnan.github.io/papers/kdd26-UGR.pdf)|不确定性生成推荐近邻，用于查对预算信号；不因名称含不确定性而标为潜在推理。|

未完成的来源核实见[待核实清单](pending-papers.md)。其他搜索命中的通用RL、编码或跨领域论文只作为检索线索，不作为方法结论依据。

### 链接检查补充

2026-09-15：迁移后的公开文档与笔记共711处链接检查，710处通过；范围外CoDeR+的ACM DOI重定向返回403，重试及网页访问仍受限，保留原始正式DOI并标记访问限制。内部链接检查全通过。该访问限制不等于论文不存在，也未将403加入成功状态。
