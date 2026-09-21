# 综述配置核读与文献回流：2026-09-21

本轮从现有100篇清单出发，定向检查过程监督、部署、预算和有效性；补历史遗漏，不宣称穷尽检索。日期取首次提交；会议未独立核实则保留 arXiv。全部结果为作者报告，本仓库未复现。

## 新增与资源变化

| 论文 | 首次提交 | 固定证据 | 归类与资源 |
| --- | --- | --- | --- |
| CogRec：SID 结构路由 | 2026-07-27 | [v1 方法、§4 与表4](https://arxiv.org/html/2607.24402v1) | 核心 CoT；[官方代码](https://github.com/caskcsg/CogRec) 页面已核，未运行 |
| CogRec：Soar 智能体 | 2025-12-30 | [v1 摘要与方法](https://arxiv.org/html/2512.24113v1) | 核心智能体；规则推理参与推荐决策；官方实现未核实 |
| Restoring Collaborative Signals | 2026-07-30 | [v1 方法、评测和文本对照](https://arxiv.org/html/2607.27682v1) | 评测研究；固定骨干、候选与语言接口对照；官方实现未核实 |
| Faithful SID Evaluation（既有） | 2026-05-25 | [v2 §3–4、表4](https://arxiv.org/html/2605.25330v2) | 新核实[官方 CollisionGenRec](https://github.com/Nishikata97/CollisionGenRec)；标题更名仍按同一 ID 去重 |

新增3篇后总103篇（78核心、6基准、8评测、2综述、9背景）；精选卡片17篇不变。CogRec 路由先输出轨迹再输出 SID；多轨迹采样、历史 metadata 与直接预测存在差异。表4路由在 Sports 更好、Toys 更差，不据此声称全域或等预算提升。Restoring 的原生 CoT 诊断与主表数值来自不同实验口径，不拼接；目标隔离子集也不与全体混用。

## 过程与监督

- [HiLaR v1 §4.3，式14–16](https://arxiv.org/html/2607.27760v1)：逐状态目标对数概率增益经裁剪、加权后进入总奖励；优势与策略比率为轨迹级。作者的层级奖励不等于每层独立优势。输出是物品标题。[作者仓库](https://github.com/hupeiyu21/HiLaR)仍为占位 README。
- [SAPO v1 §3、附录L表7](https://arxiv.org/html/2605.17648v1)：先生成全部思考块再输出 SID，训练按思考—SID 配对计算步骤优势。Office 短程计时不能当收敛成本。附录表6标题 BF16 与 Stage3 精度 FP32 表项不一致；保留该疑点。作者入口 `https://github.com/zhengzaiyi/SAPO` 访问404（链接检查失败记录，非可用实现）。
- [PROMISE v1 表4](https://arxiv.org/html/2601.04674v1)：前缀 PRM 的部署层数改变搜索筛选位置；更多层评分同时增加计算，不能仅凭召回提升称为等预算优势。
- [S²GR v3 §4、附录B](https://arxiv.org/html/2601.18664v3)：Beauty 测试另过滤长度不足10的序列；同名数据集不能直接横比。潜在监督移除属于训练消融，非固定状态的因果忠实性干预。
- [CaLIR v1 §4.2.3 式22](https://arxiv.org/html/2606.07075v1)：已显式使用多正类别原型的对比目标。多正例不是完全无人研究；其电商查询目标仍不同于单点击过程奖励的误奖罚问题。

## 部署与成本

- [OneRec-Think v2 §4.4/5.4](https://arxiv.org/html/2510.11639v2)的工业方案离线生成理由及 SID 前缀，线上补全末级；[ACL正式版](https://aclanthology.org/2026.acl-long.123/)表2新增 Toys 消融。不能用公共数据的准确率配工业训练成本。官方代码 commit `4c573ac6dd6e7d8a1ee4152083e4e07928de1d92` 树未见 GRPO 训练入口，不能当完整复现。
- [TGR v1 §5](https://arxiv.org/html/2609.00986v1)：表16是三日期等权离线评估；表17另有线上 A/B。默认部署 DRI-only，不含 GMR；latent 用于训练，导出 K=0。§5.3.3 的174→80分钟是离线刷新，工作量分母未充分公开，不能换作单请求时延。
- [SelfDR v1 表4/6/7](https://arxiv.org/html/2609.03313v1)：训练集目标条件教师、测试集学生与2000例成本抽样分开。SASRec top20不保证正例；单 A800 的109.46ms/例与54.18小时总训练不是工业上线测量。
- [LASAR v2 表3/4、附录F](https://arxiv.org/html/2605.10207v2)：平均latent深度不等于实际批处理成本，短样本有padding；GREAM主表direct模式不能搭配CoT模式成本。
- [IBA v1 表V](https://arxiv.org/html/2607.12425v1)：Instruments六步与八步的质量和生成时间可分别同表配对；预算先验同时变化，不能把差异全归因于步数。分配在解码前完成，非逐步自适应停止。
- [CARE v2 表1/4/5](https://arxiv.org/html/2602.03692v2)：query在阶段内并行；效率表训练batch1024、主表默认512，因此效率配置质量保留未知。
- [Diffusion-GR2 v4 表3](https://arxiv.org/html/2607.01170v4)：阈值.9对应R@1=.2950、172tok/s；.6对应.2942、234tok/s。仅十候选文本重排的解码吞吐，非全目录latent生成或端到端加速。

## 有效性与排除边界

[Disconnect v1](https://arxiv.org/html/2608.23154v1)的SID/标题接口、训练阶段和奖励梯度掩码须分别登记；轨迹描述评分不等于因果忠实性，也不能将个别设置的退化泛化到所有推荐推理。[SIDScope v1 表5](https://arxiv.org/html/2608.18779v1)区分同结构前缀诊断与训练后生成器关联；前者相关性不能自动迁移。Faithful SID Evaluation 的CCE是假设碰撞组内均匀次序的物品指标期望，不等于实测消歧，也不检验latent语义。

扩检参考的[曝光偏差基础研究](https://proceedings.mlr.press/v48/schnabel16.html)与[NLP推理预算研究](https://arxiv.org/abs/2408.03314)仅作综述理论背景，不加入推荐核心清单。普通tokenizer、曝光公平或事后解释工作不能仅凭关键词纳入；尚未核实的候选不作为反例或已证实空白。
