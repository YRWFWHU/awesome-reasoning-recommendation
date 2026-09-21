# 2026-09-21 综述准备阶段的文献回流

本轮以现有97篇为种子，做全时段回溯补漏；并非声称新发现的三篇都在最近一周发表。新增2篇核心方法、1篇综述，总100篇（76核心、6基准、7评测、2综述、9背景）；精选卡仍17篇。未运行论文实验复现。

| 文献 | 首次日期/核读版本 | 一手证据与阅读范围 | 资源和结论边界 |
|---|---|---|---|
| CARE | arXiv v1 2026-02-03；核读v2 | [摘要历史](https://arxiv.org/abs/2602.03692)、[正文§2–3](https://arxiv.org/html/2602.03692v2) | 论文链接的[作者仓库](https://github.com/Linxyhaha/CARE)包含实现；未运行。仓库称WWW26，本轮未独立核正式出版，仍标arXiv。并行query不同于串行rollout。 |
| Diffusion-GR2 | arXiv v1 2026-07-01；核读v4 | [摘要历史](https://arxiv.org/abs/2607.01170)、[正文§2.1、3.4–3.6、4.1–4.3](https://arxiv.org/html/2607.01170v4) | 文字CoT与10候选排列；Beauty，1615测试用户；资源未核实。吞吐设置为H100-80G和torch.compile，不外推为服务端到端加速；不将不同阈值的质量和成本拼接。 |
| Towards Reasoning-Aware Recommender Systems | TechRxiv v1封面2025-11-11；v2封面2025-11-17 | [作者主页](https://junliang-yu.github.io/publications/)指向TechRxiv；官方固定PDF的§II-C/Fig2/III–VI | 完整作者Jiaqi Zhang、Junliang Yu、Zongwei Wang、Wei Yuan、Tong Chen、Quoc Viet Hung Nguyen、Bin Cui、Hongzhi Yin。预印本，不能标TKDE发表。 |

## TechRxiv可追溯标识与访问限制

DOI：`10.36227/techrxiv.176287939.92578520/v2`。

固定v2 PDF原地址：`https://d197for5662m48.cloudfront.net/documents/publicationstatus/291203/preprint_pdf/59eeb9f727d8364602b716f79f0c2349.pdf`。

固定v1 PDF原地址：`https://d197for5662m48.cloudfront.net/documents/publicationstatus/289995/preprint_pdf/75bc762bdd1fbb3228344ed60caa9ea5.pdf`。

检索代理成功读取两版封面与v2正文；TechRxiv落地页/DOI在浏览工具报Internal Error，根代理重开固定PDF和curl也遇到访问失败。因此首页保留可访问的作者论文入口，并在此保存原标识和限制，不把PDF描述为稳定可用资源。日期是该预印本平台首次公开口径，不保证全球最早。

## 其余候选的处理

已有Agentic Roadmap不重复添加。Data/Model/Tasks、Modular SID、Tri-Decoupled GenRec及通用Latent CoT四篇综述用于研究定位，但范围较广，本轮不扩张公开核心清单。Textual Explainable Recommendation in the Era of Large Language Models尚未核完整论文，留待核；DLMRec仅以扩散/生成本身不足以证明匹配范围，未新增。
