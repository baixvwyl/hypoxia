# 单细胞程序向 Xenium 映射：初步方法审查

日期：2026-11-16。状态：文献/源代码静态核查，尚无用户数据实测。

## 已知研究设计

小鼠T low/T high，各5只scRNA-seq、各3只Xenium，Xenium动物是前者的子集。跨模态配对依据是mouse_id，不是细胞一一对应，也不是两组动物相互配对。空间组间分析的独立生物学重复是每组3只，不能把细胞/视野当小鼠重复。

## 核查来源

- starCAT 原始论文：https://doi.org/10.1038/s41592-025-02793-1
- 作者代码固定提交：5399183aa6093ff972bb605d2e33d64ce41b944c；https://github.com/immunogenomics/starCAT
- 作者自定义参考教程：Examples/build_reference_vignette.ipynb；导出starcat_spectra，而不是直接使用marker列表或有正负值的gene scores。
- 用户提供全文：Spatial transcriptomics resolves ductal TREM2+ and stromal FOLR2+ macrophages in the normal human breast at microanatomical resolution；https://doi.org/10.64898/2026.08.05.742266；PDF说明为2026-08-06发布的预印本，未同行评议。

## 已核实事实

starCAT接受自定义program×gene非负参考，固定参考后估计query的非负程序usage；作者实现使用scikit-learn non_negative_factorization，update_H=False，Frobenius loss。query要求原始非负counts，在共同基因上按基因做不中心化的方差缩放。默认返回usage按细胞归一至和为1；这不是分类置信概率。

巨噬细胞文献在scRNA-seq中用cNMF构建参考，再用starCAT投射Xenium（Fig.4；Methods “Consensus non-negative matrix factorization and reference-query mapping”）。采用5K加定制面板；正文共同基因数为687，Methods为673，两处不一致，不能据此设定通用最低基因数。

当前starCAT README明确表示其全转录组参考在限制基因面板的探针平台上可靠性尚未确立。这与特定预印本应用先例须分开陈述。

## 针对本项目的建议（待数据验证）

保留现有3CA结果作为发现和解释层，先确认3CA输出到底是标签、基因集合还是可用的非负谱矩阵。只有marker/top基因集合时不能直接转成可靠的starCAT参考；优先在本项目小鼠、分谱系的scRNA-seq中构建兼容参考，并与3CA程序对齐，不把人T细胞TCAT默认参考直接用于小鼠髓系/肿瘤细胞。

先定大类细胞，再在谱系内估计连续程序usage；离散亚型标签单独验证。参考训练应兼顾两组并检查跨鼠复现，mouse_id/技术批次与生物学组别分开，不能把目标组别差异一律校正掉。

先计算每个程序的面板覆盖、权重覆盖和截取后程序间可分性。按小鼠留出建立参考，在留出小鼠中比较全转录组和仅面板基因得到的usage/标签；不能随机拆同一只鼠的细胞声称跨鼠验证。该实验只检查面板信息损失，不消除Xenium检测效率、分割和污染差异。

对有Xenium的动物，可用不包含该动物的参考产生交叉拟合的空间结果；若最终参考使用全部10只小鼠，必须标明配对内部映射，不能将这6只当独立外部验证。仅面板监督标签转移/分类和简单评分作为比较基线；不预设starCAT胜出。

置信度通过留鼠验证、程序/基因扰动稳定性、拟合残差及可判别性共同评估；低信息细胞保留不确定，不能强制归入最高usage的类别。空间统计在切片内构图，按小鼠汇总效应，再比较每组3只；明确空间邻域效应与细胞比例差异。

## 当前所缺输入

3CA脚本或软件版本与输出示例；Xenium面板；scRNA原始counts与cell metadata；Xenium counts、坐标、分割/QC和mouse_id/section_id；T的定义。未执行生物学分析。后续本次阅读已建立正式证据包并通过结构校验；复现仍为材料冲突/受阻，见[证据包](../reconstructions/starcat-xenium-review/README.md)。


## 用户补充与方案修订

用户确认：Xenium为5K面板；T low/T high指T细胞浸润；Omicos 3CA在每个大类内逐样本跑NMF，然后跨样本得到一致性MP。因此与starCAT的发现程序/投射程序思路兼容，尚不能据此确认输出文件可直接作为reference。

优先保留现有MP。先检查原始单鼠NMF谱、usage、MP成员映射及是否有完整非负共识谱；不能用top-gene列表或有符号分数替代已校准参考。若保留基因权重，核对各样本预处理和尺度，再构建/校准参考；如只有MP基因集，可将其用于匹配与解释独立构建的cNMF参考，避免声称任意矩阵改格式就可直接使用。程序匹配不强制一对一。

5K提供更多潜在覆盖，不代表每个MP都能识别。优先检查每个MP的权重覆盖及面板投影后共线性；使用小鼠自身参考，不直接使用人TCAT。单细胞整鼠留出验证需从程序发现/参考构建阶段排除留出鼠，单独在末端分类器留出不足以避免泄漏。

T浸润作为分组指标时，T细胞丰度差异是分组定义相关观察，不能当作独立发现；重点考察其他谱系的程序及其空间关联，区分总体T细胞丰度与局部邻域富集。需记录分组测量来源、阈值、取样区域及Xenium子集选择。
