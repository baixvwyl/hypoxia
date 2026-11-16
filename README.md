# hypoxia
hypoxia xenium

## 文献阅读入口

本仓库用于小鼠PDAC的单细胞—Xenium程序映射与缺氧生态位研究。当前已完成两篇文献的阅读整理及选定方法的静态审查；尚未取得项目表达矩阵，也未执行3CA转换或Xenium映射。

| 内容 | 入口 |
| --- | --- |
| starCAT原论文：原理、参考构建、代码行为与适用边界 | [P001阅读笔记](literature/notes/P001-starCAT-2025.md) |
| 正常乳腺巨噬细胞：非T细胞starCAT→Xenium应用 | [P002阅读笔记](literature/notes/P002-macrophage-Xenium-2026.md) |
| 对本项目的具体判断与下一步材料 | [从阅读进入分析](docs/reading-to-analysis.md) |
| 初步方法审查及用户补充 | [映射可行性记录](docs/starcat-mapping-assessment.md) |
| 文献台账 | [papers.tsv](literature/papers.tsv) |
| 论文—图—方法—代码证据包 | [证据包说明](reconstructions/starcat-xenium-review/README.md) |

目前最关键的结论：保留已有3CA MP，先确认其完整非负谱与尺度，再评估是否能用于starCAT。5K面板仍需逐MP检验可识别性；MP usage不等同离散亚型或分类概率。

## 当前证据状态

2026-11-16使用固定版本的上游校验器完成检查：**结构和证据契约校验通过，0 errors、0 warnings**。这不表示生物学复现成功。

- 巨噬细胞Fig.4B：**材料冲突**。正文报告687个共同基因，Methods报告673；还缺作者参考与分析输入。
- starCAT投射算法：**受阻**。已核查方法和固定源码，未取得用于数值复现的输入、历史环境与运行记录。
- 本项目数据分析：**未开始**。没有生成空间细胞标签或程序usage。

## 如何继续用文献阅读框架

参考[LCGaoZzz/bioinfo-protocol-reconstructor](https://github.com/LCGaoZzz/bioinfo-protocol-reconstructor)，本仓库将其作为固定提交的子模块。可对协作助手提出：“按本仓库AGENTS.md，读取指定论文，更新阅读笔记和证据包；没有原始数据时只做审查，不声称复现。”

```bash
git clone --recurse-submodules https://github.com/baixvwyl/hypoxia.git
cd hypoxia
python -m pip install -r requirements-framework.txt
```

先阅读[工作规则](AGENTS.md)和[上游SKILL.md](framework/bioinfo-protocol-reconstructor/skills/dev-reconstruct-bioinfo-protocol/SKILL.md)，按材料盘点、跨材料对齐、复现审查的顺序工作。证据不足时保留缺口，不补造参数。

PDF、全文提取和大型原始数据未提交。已发布的校验报告来自本地完整证据快照；要重新进行哈希校验，需要按[来源说明](reconstructions/starcat-xenium-review/PROVENANCE.md)恢复`source_inventory.json`列出的材料。仅克隆仓库不能重现当时的本地文件校验。
