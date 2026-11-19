# Greenwald 2024：layer 流程证据包

本次审查对应 Cell 论文 *Integrative spatial analysis reveals a multi-layered organization of glioblastoma*，用于判断其方法对小鼠 PDAC 单细胞—Xenium 项目的适用性。

- [完整阅读笔记](../../literature/notes/P003-greenwald-glioma-layers-2024.md)：论文流程、五层含义、Methods 与活动代码差异。
- [本项目方法评估](../../docs/layer-analysis-for-pdac-xenium.md)：3CA 保留条件、映射接口、Xenium 邻域、按鼠验证和统计边界。
- [traceability.tsv](traceability.tsv)：论文—图—Methods—代码—输入输出对应表。
- [reconstruction_manifest.json](reconstruction_manifest.json)：五个分析的结构化证据与科学审查。
- [REPORT.md](REPORT.md)：由 manifest 生成的状态与未解决问题；没有本次数据运行产生的生物学解释。
- [PROVENANCE.md](PROVENANCE.md)、[source_inventory.json](source_inventory.json)：原始来源、固定版本、定位和 SHA-256。
- [working_state.json](working_state.json)、[validation_report.json](validation_report.json)：可续接状态及结构校验记录。

## 当前状态

2026-11-19：固定上游验证器 `dev-reconstruct-bioinfo-protocol/1.4.0` 校验通过，**0 errors、0 warnings**。已完成材料盘点及跨材料对齐；复现审查保留冲突和输入缺口。没有执行作者 R 分析、用户 3CA、starCAT 或 Xenium 空间分析。

| analysis_id | 审查内容 | 复现状态 |
| --- | --- | --- |
| MP_ANNOTATION | MP 发现与 spot 注释 | 材料冲突 |
| SPATIAL_ZONES | 空间一致性与组织区域 | 受阻 |
| MULTISCALE_COUPLING | 同点、邻接及区域组成关联 | 材料冲突 |
| CODEX_NEIGHBORHOODS | 真实细胞邻域分析 | 材料冲突 |
| LAYER_GRAPH | 多尺度网络与层次模型 | 材料冲突 |

校验通过只说明证据契约、定位、哈希和状态一致，不表示公式正确、代码可完整重跑或结论已在 PDAC 验证。正式报告中解释项为空，是因为当前停留在静态审查阶段；来源归纳及方法适用性见上方两份文档。

## 复核

先按来源清单恢复本地只读快照，再在仓库根目录运行：

```bash
python framework/bioinfo-protocol-reconstructor/skills/dev-reconstruct-bioinfo-protocol/scripts/validate_reconstruction.py \
  --project-dir reconstructions/greenwald-2024-layers --write-report
```

`sources/` 中的全文、图像和用户上传材料未提交。`available` 表示审查时本地存在并已核对哈希，不意味着仅克隆仓库就能重跑全部来源校验。预期的 `inputs/`、`outputs/` 路径不是已生成文件；作者 Inputs.zip 公开可获取，但本次尚未下载核对。
