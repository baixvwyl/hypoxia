# starCAT—Xenium文献审查证据包

日期：2026-11-16。请求范围：阅读并整理文献，重点审查巨噬细胞论文Fig.4B和starCAT固定参考投射算法。不是整篇所有图的计算复现；没有执行生物学分析。

## 阅读与机器检查分别看哪里

| 文件 | 用途 |
| --- | --- |
| [两篇中文笔记](../../literature/notes/) | 研究问题、证据结构、方法、限制和项目适用性 |
| [traceability.tsv](traceability.tsv) | 每行一个分析，连接正文、图、Methods、代码、I/O和缺口 |
| [reconstruction_manifest.json](reconstruction_manifest.json) | 结构化证据、参数、八项科学审查及复现状态 |
| [source_inventory.json](source_inventory.json) | 本地来源、SHA-256及提取限制 |
| [working_state.json](working_state.json) | 已达阶段与阻塞项 |
| [REPORT.md](REPORT.md) | 上游固定格式的状态/缺口报告 |
| [validation_report.json](validation_report.json) | 本地源文件存在时的校验结果 |
| [PROVENANCE.md](PROVENANCE.md) | URL、PDF来源、固定提交与恢复说明 |

材料盘点和跨材料对齐已完成；复现审查因冲突/缺失而停在partial；执行/代码指导和生物学解释阶段未开始。按上游规则完成了阻塞项目的校验交付。没有调用Omicos工具，用户的3CA实现尚未审阅。

`REPORT.md`的解释栏为空是阶段门槛的结果，不代表没有阅读论文。论文内容归纳在阅读笔记，科学审查在manifest；没有将尚未运行的分析包装为重建支持或新生物学结论。

## 状态

- `MAC_F4B`：材料冲突。687与673共同基因的记载冲突未解决；作者reference、query和结果对象亦未取得。
- `STAR_PROJECTION`：受阻。算法静态检查完成，但缺数值复现输入与历史环境。
- 整体：材料冲突。

正式校验结果：valid=true，0 errors、0 warnings。此结果只检查证据契约与本地文件一致性，不认证论文生物学正确性，也不表示程序已经运行。

## 本地重新校验

先初始化仓库子模块、安装`requirements-framework.txt`，再按来源说明恢复被Git忽略的`sources/`快照。随后从仓库根目录运行：

```bash
python framework/bioinfo-protocol-reconstructor/skills/dev-reconstruct-bioinfo-protocol/scripts/validate_reconstruction.py --project-dir reconstructions/starcat-xenium-review --write-report
```

缺原始材料时应保留已有报告作为历史记录；若重新运行得到失败，不应删除失败或改写来源为“已验证”。公开网页或软件版本更新后，重新获取的字节可能不同，需要保留新版本并重新审查来源。
