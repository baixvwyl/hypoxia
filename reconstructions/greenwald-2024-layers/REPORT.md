# Reconstruction report

## Status

- MP_ANNOTATION: 材料冲突

- SPATIAL_ZONES: 受阻

- MULTISCALE_COUPLING: 材料冲突

- CODEX_NEIGHBORHOODS: 材料冲突

- LAYER_GRAPH: 材料冲突

## Direct evidence/observation

- none

## Paper claim

- none

## Reconstructed support

- none

## Reasonable inference

- none

## Unverified

- none

## Conflicts or gaps

- MP_ANNOTATION/MP_C01 (conflict): Methods同样本稳健重叠为30/50，Module1活动调用intra_min=35，函数默认则为30。 [evidence: MP_ANNOTATION_M, MP_CODE]

- MP_ANNOTATION/MP_G01 (gap): 作者公开Inputs.zip尚未获取；表达、预计算MP、最终注释和历史运行记录缺失，列出路径均为预期占位。 [evidence: MP_ANNOTATION_M, MP_CODE]

- SPATIAL_ZONES/ZONE_G01 (gap): 缺spot注释、组织边界、CNA、鼠/患者及切片元数据与输出对象；路径是预期占位。 [evidence: SPATIAL_ZONES_M, ZONE_CODE]

- SPATIAL_ZONES/ZONE_G02 (gap): 代码局部计算对高丰度程序改变归一方式并有最少spot数等分支；未取得实际中间对象和执行环境。 [evidence: SPATIAL_ZONES_M, ZONE_CODE]

- MULTISCALE_COUPLING/COUP_C01 (conflict): Methods写共定位效应expected/observed，活动代码r1为observed、r2为expected并计算r1/r2。 [evidence: MULTISCALE_COUPLING_M, COUP_CODE]

- MULTISCALE_COUPLING/COUP_C02 (conflict): Methods称Fisher精确检验，共定位和区域相关活动代码使用Fisher z形式变换与正态尾概率。 [evidence: MULTISCALE_COUPLING_M, COUP_CODE]

- MULTISCALE_COUPLING/COUP_G01 (gap): 未获取作者实际输入、分区运行配置、逐样本结果和完整检验族；占位路径不存在。 [evidence: MULTISCALE_COUPLING_M, COUP_CODE]

- CODEX_NEIGHBORHOODS/CODEX_C01 (conflict): Methods将A周围B总数除以A细胞数；代码汇总后除以A所有非自身类型邻接计数。 [evidence: CODEX_NEIGHBORHOODS_M, CODEX_CODE]

- CODEX_NEIGHBORHOODS/CODEX_G01 (gap): 作者细胞对象、配准说明、原始结果和历史运行配置未取得；当前活动调用只确认27.5微米与500次。 [evidence: CODEX_NEIGHBORHOODS_M, CODEX_CODE]

- LAYER_GRAPH/LAYER_C01 (conflict): Methods按每种测量的阈值及支持数量筛选；Module4还要求跨测量总体pair_mean>0.35的pattern为connected。 [evidence: LAYER_GRAPH_M, LAYER_CODE]

- LAYER_GRAPH/LAYER_G01 (gap): 已检查Modules1、2、3、4、6未定位完整的任意两种测量扩展网络到最终layer分配与Cytoscape布局代码链。 [evidence: LAYER_GRAPH_M, LAYER_CODE]

- LAYER_GRAPH/LAYER_G02 (gap): 缺实际Summary_tables、最终网络及历史运行对象，所列输入输出为占位。 [evidence: LAYER_GRAPH_M, LAYER_CODE]
