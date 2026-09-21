# 过程反馈与评测协议定向补证：2026-09-21

本轮从103篇冻结索引补历史遗漏，未进行全领域穷尽检索。新增1篇后总104篇（79核心、6基准、8评测、2综述、9背景），17篇精选卡片不变。

## 新增 Flower

[Process-Supervised LLM Recommenders via Flow-guided Tuning](https://arxiv.org/abs/2503.07377)，首次提交2025-03-10；[固定v3](https://arxiv.org/html/2503.07377v3)，正式DOI `10.1145/3726302.3729981` 的[Crossref记录](https://api.crossref.org/works/10.1145/3726302.3729981)对应SIGIR 2025、1934–1943页，出版元数据由Crossref/DOI核实。ACM落地页在浏览器及链接检查中均返回403，公开入口采用可访问的出版方登记元数据；固定论文正文由arXiv读取。

§3.3把叶物品奖励向上汇总，再以子/父节点流比形成标题分支监督；§3.4的实际目标结合SFT与SubTB，不能仅按摘要称其完全移除SFT。§4.1.4的偏好分数来自SASRec。该方法与过程监督及生成路径直接相关，纳入奖励设计；它没有独立的latent思考状态，经验频率拟合也不等于曝光去偏。

[官方仓库](https://github.com/Mr-Peach0301/Flower)由论文链接确认，包含with_history和without_history源码、训练及评测脚本；作者说明训练集文件未上传并提供预处理步骤。只核源码可用性，未运行实验。

## 既有条目的协议纠正

- **CogRec路由**：[v1 §4.1.3–4.1.4与表4](https://arxiv.org/html/2607.24402v1#S4.SS1.SSS3)。[固定代码](https://github.com/caskcsg/CogRec/blob/174da662799d24ed9f031ade9e8ce5cd12d7c6b7/test/precompute_global_trie.py#L65-L83)从完整测试历史与目标SID建立全局并集，未直接读取全目录映射；尚无集合计数证明二者相等。全局并集不是逐用户强制注入目标的证据。[子集函数](https://github.com/caskcsg/CogRec/blob/174da662799d24ed9f031ade9e8ce5cd12d7c6b7/data/hnsw_and_splits.py#L667-L701)默认抽10%、seed42，但论文表4未绑定运行日志，不能将该默认直接赋给表中数值。同Stage3检查点也可评No-CoT，Direct不必等于Stage2。
- **TGR**：[v1 §5.2.3](https://arxiv.org/html/2609.00986v1#S5.SS2.SSS3)明确DRI不改变SID决策数或beam-search space；缓存是条件。[§5.4.1](https://arxiv.org/html/2609.00986v1#S5.SS4.SSS1)的独立SID直取支路与DRI生成支路不同。具体生产目录/过滤边界仍未知，表16不自动覆盖所有支路。
- **Diffusion-GR2**：[v4 §4.1与表3](https://arxiv.org/html/2607.01170v4#S4.SS1)的1615用户选择、召回器和目标覆盖仍未知。[原始GR2 v6 §5.4](https://arxiv.org/html/2602.07774v6#S5.SS4)虽说明Beauty使用Qwen3-8B MTL召回，其pre-rank R@1=.2892与Diffusion的.2811不同，不能自动视为同一配置。两者均已收录。

## 其他候选处置

- [RGD v1 §4.2.2–4.2.3](https://arxiv.org/html/2607.25344v1#S4.SS2)：已收录；逐SID层奖励头使用曝光条件的点击/长观看/关注/送礼监督，并融合多个业务目标。该训练样本口径不自动识别未曝光物品的反事实效用。
- [CaLIR v1](https://arxiv.org/html/2606.07075v1)、[HiLaR v1](https://arxiv.org/html/2607.27760v1)、[RPORec v1](https://arxiv.org/html/2605.21967v1)：已收录；分别用于区分多正类别、目标增益和复合奖励，不重复添加。
- [DualGR v3](https://arxiv.org/html/2511.12518v3)：范围外近邻。曝光未点击的SID负学习与独立推理过程奖励不同，不因出现曝光和奖励词汇进入核心清单。

本轮没有获得论文实验结果或复现；候选协议的源码核读不等于测出其偏差幅度。公开文献与来源更新在本仓库，未发表综述稿件保留本地。
