# P001｜starCAT 原论文阅读笔记

**文献**：Kotliar D, Curtis M, et al. *Reproducible single-cell annotation of programs underlying T cell subsets, activation states and functions.* Nature Methods (2025). DOI：[10.1038/s41592-025-02793-1](https://doi.org/10.1038/s41592-025-02793-1)。[开放全文](https://pmc.ncbi.nlm.nih.gov/articles/PMC12446064/)。PMID 40903640。

**阅读日期**：2026-11-16。已阅读正文、相关图注与方法，重点核查程序发现、共识参考及query投射。正式证据包分析ID为 `STAR_PROJECTION`；未逐图重建全部分析，也未运行作者数据。

## 研究问题与方法贡献

作者希望把“细胞是什么”和“细胞正在经历什么状态”分开表达。离散聚类可能由增殖、干扰素、细胞毒性或技术质量等程序主导，掩盖同一簇中不同的细胞身份。starCAT用多个可共存的表达程序usage描述每个细胞，再按需要增加分类器或功能评分。

需要区分三个对象：cNMF是发现程序的方法；starCAT是用固定程序参考注释query的工具；TCAT是论文构建的人T细胞参考及相关评分。论文说明star中的星号代表可扩展到不同组织与细胞类型，不能由此推定任意参考在任意平台上都有效。[Results “Annotating cells with predefined GEPs”；本地文本L20、L26–29]

## 正文证据结构

| 部分 | 作者做了什么 | 本项目应如何使用这项证据 |
| --- | --- | --- |
| Fig.1与Methods | 分数据集cNMF发现程序，跨数据集聚合为共识程序，固定参考注释query | 支持“先发现、后投射”的设计；与逐样本NMF再归并MP的思路相容 |
| Fig.2 | 在独立人T细胞CITE-seq数据中，用蛋白门控标签评价亚群分类 | 提醒我们需要独立于RNA程序的验证；不能照搬其准确率到小鼠Xenium |
| Fig.3 | 展示多个身份、功能与质量程序在同一细胞中共存 | MP不必是互斥亚型；不宜简单argmax后丢弃其余usage |
| Fig.4 | AIM-seq刺激实验研究与TCR依赖激活有关的程序 | 是针对T细胞激活的实验支持，不是巨噬细胞或缺氧程序的验证 |
| Fig.5 | 构建ASA评分并分析疾病中的激活、耗竭等状态 | 使用了针对人T细胞校准的派生规则，不能直接作为小鼠通用阈值 |
| Fig.6 | 分析程序与免疫检查点抑制治疗反应的关系 | 属于特定队列中的关联/预测证据；不等于本项目的因果机制 |

上表为正文/图注阅读索引，除正式证据包所列分析外，不声称完成了各图的代码审计或数值验证。

## 核心计算到底是什么

设表达矩阵为细胞×基因，程序谱为程序×基因。cNMF同时估计细胞usage和程序谱；starCAT保持谱不变，只拟合query的非负usage，最小化重构误差。

Methods “starCAT algorithm”明确报告：Frobenius误差、multiplicative update (`mu`)求解器、容差 `1e-4`、最多 `1000` 次迭代；使用scikit-learn `1.1.3`。query按基因标准差缩放；最终每个细胞的usage归一化到总和为1。[本地文本L123–126；证据STAR_M]

**usage不是分类概率，也不是某一功能的直接测量值。** 原始usage、归一化usage、附加评分与离散标签应分别保存和解释。归一化后一个程序增加也可能压低其他程序的相对usage。

## 参考谱不能由marker列表直接替代

论文为不同用途保存不同的谱表示。共识参考构建从表达谱出发，调整表达尺度并按基因变异缩放，再对跨数据集匹配的程序取平均；用于marker解释的z-score谱是另一种表示。[Methods “Constructing a catalog of cGEPs”；本地文本L135–141；STAR_REF]

因此，3CA给出的top genes、富集分数、logFC或z-score不能仅改成TSV就视作可用reference。需检查完整非负谱、原始NMF的缩放规则、MP的成员关系和合并方式。保留MP的生物学解释，与构建可投射的数值参考，是相互关联但不同的工作。

## 作者代码核查

核查快照：[5399183aa6093ff972bb605d2e33d64ce41b944c](https://github.com/immunogenomics/starCAT/tree/5399183aa6093ff972bb605d2e33d64ce41b944c)。这是阅读时固定的源码快照，不能当作论文发表时的完整执行环境。

| 源码位置 | 静态核查结果 |
| --- | --- |
| [starcat.py L19](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py#L19) | 核心参数与上述求解设置相符，`update_H=False`固定参考谱 |
| [L80](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py#L80) | `.txt`/`.tsv`路径可作为自定义参考 |
| [L227](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py#L227) | 检查query非负性；对非整数counts发出提示；只取共同基因，再按基因缩放，不中心化 |
| [L199](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py#L199) | 默认返回逐细胞归一化usage；可选返回未归一化usage |
| [L272](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py#L272) | 将参考作为固定H传入`non_negative_factorization` |

作者[当前README](https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/README.md)明确说明：其全转录组参考在限制基因面板的探针平台上的可靠性尚未普遍建立。README提到的测试依赖版本与论文Methods版本应分别记录，这是不同时间材料的版本差异，不能自动推定论文错误。

[TCAT_analysis](https://github.com/immunogenomics/TCAT_analysis/)提供原论文分析。此次检查了仓库目录结构与图索引入口；没有将其中T细胞分析脚本误当作后续巨噬细胞论文的脚本，也未完整审计所有notebook。

## 对本项目的审查结论

保留现有逐鼠NMF与跨鼠MP结果，有理由进一步检查其是否能转换为兼容参考。软件名称或NMF实现不同，本身不足以否定投射路线；真正的门槛是谱的含义、尺度和面板中的可辨识性。使用小鼠自身、分谱系构建的参考更符合当前设计；人T细胞TCAT参考不能直接代替小鼠全组织参考。

正式状态为**受阻**：缺输入参考、query、历史环境和运行记录；这是复现状态，不表示论文不能阅读或方法不可用。详见[证据包](../../reconstructions/starcat-xenium-review/README.md)与[项目适用性审查](../../docs/starcat-mapping-assessment.md)。
