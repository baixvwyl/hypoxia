# 来源与版本记录

阅读/核查日期：2026-11-16。原始材料只读；公开仓库保存整理产物，不发布上传PDF或全文快照。

## 用户上传的巨噬细胞论文

- 文件名：`2026.08.05.bioxv，starCAT 乳腺巨噬细胞.pdf`
- DOI：https://doi.org/10.64898/2026.08.05.742266
- PDF字节SHA-256：`4664bb14e24eaf9a1db4413be8b3ec6364fa12eb573bb8cc08c66897f74f8d97`
- PDF标注：版本发布于2026-08-06，预印本，CC-BY-NC 4.0。
- `SRC001`：`pdftotext -layout`提取全文；保留分页符。双栏可能交错，定位需结合PDF页码。
- `SRC002`：`pdftoppm -f 7 -singlefile -scale-to 1700 -png`渲染第7页，实际查看Fig.4；没有像素数值提取。

## starCAT原论文与源码

- 论文：https://doi.org/10.1038/s41592-025-02793-1
- 开放全文：https://pmc.ncbi.nlm.nih.gov/articles/PMC12446064/
- XML来源：https://www.ebi.ac.uk/europepmc/webservices/rest/PMC12446064/fullTextXML
- `SRC003`：从XML提取article-title/title/p/label文本，合并段内空白；公式与图注存在重复表示，不以提取后的行号代替原文Methods标题。
- `SRC004`：https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/src/starcat/starcat.py
- `SRC005`：https://github.com/immunogenomics/starCAT/blob/5399183aa6093ff972bb605d2e33d64ce41b944c/README.md
- TCAT分析入口：https://github.com/immunogenomics/TCAT_analysis/ 。此次仅检查目录与图索引入口；其notebook不构成巨噬细胞论文分析代码证据。

## 框架与校验

- 来源：https://github.com/LCGaoZzz/bioinfo-protocol-reconstructor
- 固定提交：`a36a5444d92e2a605bb12bf19956d2d7857ec865`
- 使用技能：`skills/dev-reconstruct-bioinfo-protocol/SKILL.md`；实际读取workflow、evidence-contract、modality-audit及manifest schema，运行其原始validator。
- 验证器标识：`dev-reconstruct-bioinfo-protocol/1.4.0`。
- 分析执行记录为空；只有文本提取、源码静态核查及证据包校验。未运行starCAT/cNMF。

## 如何理解available与复核限制

`source_inventory.json`中的available表示本次本地审查确有该快照，SHA-256已经与文件核对；不表示快照被Git追踪。`validation_report.json`是该次本地完整材料状态的记录。仓库克隆不含`sources/`，直接重跑校验会报告缺失文件。

复核时将相同版本材料放回清单列出的相对路径，核对SHA-256后再运行校验器。可以用上述命令重新提取PDF和渲染图片，但工具版本、PDF修订或文字规范化可能改变字节；不匹配时不要改哈希掩盖差异，应保留新快照并重建受影响定位与审查记录。源码提交固定，但也应核对UTF-8及换行。若仅需阅读结论，可直接阅读已发布笔记与证据表。
