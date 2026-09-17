# 2026-09-17 方法选题检索回流

先查本仓库84篇已有清单，origin/main与本地均为54dde37；保留未跟踪AGENTS.md。本轮新增6篇（3核心、3必要背景），另更新OneRec-Think正式版链接。研究候选与评审不公开。

|文献|日期与核实范围|范围判定/资源|
|---|---|---|
|[EPIC](https://arxiv.org/abs/2609.03522)|2026-09-03首发，v1摘要、引言、方法目录|物品后验进入SID中间决策，核心结构化推断；不是连续latent CoT，代码未核实|
|[MoMoREC](https://ojs.aaai.org/index.php/AAAI/article/view/38623)|2026-03-14正式出版，官方摘要/出版页及PDF索引引言|动机推理压缩成残差SID，训练期推理；最早预印本日期未确认，采用明确标注的出版口径；代码未核实|
|[MDGR](https://arxiv.org/abs/2601.19501)|2026-01-27首发，v1摘要引言|并行码本与masked decoding，必要背景，非自动等同latent reasoning；代码未核实|
|[MADRec/MaskGR](https://arxiv.org/abs/2511.23021)|2025-11-28首发，v1摘要引言|masked SID的必要背景；[作者代码](https://github.com/snap-research/MaskGR)从论文MADRec地址重定向后核实|
|[TCA4Rec](https://arxiv.org/abs/2601.18457)|2026-01-26首发，v1摘要引言及任务定义|物品到token的软监督接口，必要背景；[作者代码](https://github.com/critical88/TCA4Rec)已打开核对|
|[OneRec-Think](https://aclanthology.org/2026.acl-long.123/)|ACL官方2026年7月记录|已有条目增补正式版，首次月份仍保留2025-10，不重复计数|

S²GR、LASAR、IBA、BARGE、LaRec、HiLaR、Latte、IntuRec、FLR、PLR、DiffuReason等已有条目保持不变。通用PLRL、传统去噪/结构化表示工作作研究背景，不扩大核心范围。OpenReview个性化编码线索被浏览器验证拦截，不能据此断言已核实或不存在近邻。

此次核读用于文献定位，未开展上述论文的实验复现。公开整理文字为原创概述，不转载论文全文。

## 查新阶段追加核实

- [MindRec](https://arxiv.org/abs/2511.12597)：首次2025-11-16；读取v2摘要、引言与§3，核对[作者仓库](https://github.com/Mr-Peach0301/MindRec)存在实现目录。旧标题与仓库标题不同但为同一工作，不重复。归入核心结构化推断/搜索；下载即用数据未核实。
- [FMRec](https://www.ijcai.org/proceedings/2025/346)、现代Hopfield、DEQ、IWAE、Twisted SMC用于通用方法先例分析，未据此扩充核心推理清单。
- [DPRM](https://arxiv.org/abs/2604.24357)、[隐藏状态推测解码](https://arxiv.org/abs/2602.21224)、[低秩反事实状态迁移](https://arxiv.org/abs/2608.15156)已核一手摘要，分别属于通用生成和世界模型，范围外，不收入推荐清单。SpecFold仅有索引线索且全文入口被验证拦截，保留待核实。
