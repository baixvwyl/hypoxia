# 来源、定位与复核限制

阅读与抓取日期：2026-11-19。固定来源的 SHA-256 均列于 [source_inventory.json](source_inventory.json)，并与 manifest 一致。全文、图像、源码快照及用户上传材料仅本地保留，不发布到本仓库。

## 论文

- DOI：[10.1016/j.cell.2024.03.029](https://doi.org/10.1016/j.cell.2024.03.029)
- PMID：38653236；PMCID：PMC11088502。
- 用户提供的 Cell 页面未成功读取；本次读取 [PMC 作者稿 HTML](https://pmc.ncbi.nlm.nih.gov/articles/PMC11088502/)，不宣称核对了出版商排版 PDF 或全部补充材料。
- SRC002 `sources/paper-pmc.html` 是抓取快照；SRC001 `sources/paper.txt` 是段落提取。定位 `P:L182` 等均基于这个固定提取，而非 PDF 页码。
- 提取方法：lxml 解析 HTML，按文档顺序选择 `//h1|//h2|//h3|//h4|//p|//figcaption`，对每个节点的 `text_content()` 执行空白合并，去掉空行，以换行连接并保留末尾换行。已验证从本地 HTML 重新提取可得到相同字节。公式可能失去排版、图注可能重复；涉及公式时结合原始 HTML 与代码。

| 文中定位 | Methods / 正文章节 |
| --- | --- |
| P:L140–L150 | Spatial Transcriptomics Analysis；Per sample clustering；Generating consensus metaprograms |
| P:L163–L170 | Spot scoring and assignment；Validation of spot annotation approach |
| P:L174–L180 | Spatial coherence；Defining organizational zones；Proximity to MES-Hyp |
| P:L182–L188 | Spot Colocalization；Spot Adjacency；Regional Composition |
| P:L190–L192 | Defining consensus interactions；Generation of layers network graph |
| P:L209–L219 | CODEX pseudospots、STalign、组织区域、Colocalization、Regional composition |
| P:L94–L98 | 五层模型正文、Fig.6 图注与组织学比较 |
| P:L111 | 因果证据局限 |

## 已查看的图像

- SRC003 `sources/F4.jpg`：[Fig.4](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/dbd8/11088502/c9f9ac6c6e3b/nihms-1982595-f0005.jpg)
- SRC004 `sources/F5.jpg`：[Fig.5](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/dbd8/11088502/e37913d99d49/nihms-1982595-f0006.jpg)
- SRC005 `sources/F6.jpg`：[Fig.6](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/dbd8/11088502/5cbd002a28a4/nihms-1982595-f0007.jpg)

图像用于定性核对主张与图示，不以像素推算原始数值。Fig.2 在本次证据包中仅使用图注。Fig.6B 的 L5 是补充示意，并非与 L1–L4 一起拍到的完整五层图像。

## 作者源码

仓库：[tiroshlab/Spatial_Glioma](https://github.com/tiroshlab/Spatial_Glioma)。固定提交 `f38f9b60ddbeefd9739e1483cbc66b2650f931d3`；取自 GitHub 文件接口的 UTF-8 文本快照。固定提交支持静态行为核对，不自动代表发表时环境或最终运行路径。

| 源 ID / 文内简称 | 文件及重点定位 |
| --- | --- |
| SRC006 | [README.md](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/README.md)：模块、输入下载和 R 测试版本 |
| SRC007 / M1 | [Module1_MP.R](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/Module1_MP.R#L260-L355)：NMF、稳健程序及预计算对象；L618–L648 注释 |
| SRC008 / M2 | [Module2_spatial_coherence_org_zones.R](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/Module2_spatial_coherence_org_zones.R#L219-L486)：局部一致性和区域 |
| SRC009 / M3 | [Module3_spatial_associations.R](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/Module3_spatial_associations.R#L99-L113)：共定位效应与检验；L422–L435 区域相关 |
| SRC010 / M4 | [Module4_consensus_interactions.R](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/Module4_consensus_interactions.R#L91-L100)：总体均值门槛；L194–L200 实际筛选 |
| SRC011 / M6 | [Module6_CODEX.R](https://github.com/tiroshlab/Spatial_Glioma/blob/f38f9b60ddbeefd9739e1483cbc66b2650f931d3/Module6_CODEX.R#L415-L433)：邻接分母；L785–L789 活动调用 |

Module 5 CNA 脚本未进行本次静态审查。已检查的六份文件没有给出完整最终扩展网络和 layer 分配链；没有据此断言仓库以外的作者材料也不存在。

作者 README 指向 [Inputs.zip](https://drive.google.com/file/d/1YFOwEDFLpyxG6WX243FNA7lnrVSaiVL-/view?usp=sharing)，并称压缩包中有配准说明。本次未下载该压缩包，因而实际 RDS、Summary_tables、历史环境和输出均是未核实材料，不应写作“作者没有提供输入”。论文另提供 GSE237183 和 [Zenodo](https://doi.org/10.5281/zenodo.8105466) 数据入口，本次未获取原始数据进行数值复现。

## 用户项目材料

SRC012 `sources/user-3ca-audit.txt` 是用户上传 `已粘贴的文本.txt` 的字节副本，报告标题为“单细胞侧 MP 实现方式与 3CA 前置步骤——溯源审计报告（只读）”，报告日期 2026-11-12。它用于说明本项目的参考尺度风险；本次没有重新审计其底层原始脚本或矩阵，不把报告陈述等同于本次执行记录。用户确认的样本设计另外记录在根目录 `project.json`。

## 框架与复核

使用仓库固定子模块 [bioinfo-protocol-reconstructor](https://github.com/LCGaoZzz/bioinfo-protocol-reconstructor/tree/a36a5444d92e2a605bb12bf19956d2d7857ec865) 的 [SKILL.md](../../framework/bioinfo-protocol-reconstructor/skills/dev-reconstruct-bioinfo-protocol/SKILL.md)、workflow、evidence-contract、相关 modality-audit 及 schema；运行未修改的上游验证器。

`validation_report.json` 记录本地快照的结构和证据契约检查，执行记录为空。只克隆仓库会缺少被忽略的 `sources/`；恢复时必须核对清单哈希。PMC 网页可能随时间变化，GitHub 接口与直接下载也可能有换行差异。新下载字节不一致时保留新版本并重新提取、审查受影响定位，不修改哈希以伪装旧快照相同。
