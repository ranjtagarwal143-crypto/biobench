# BioBench

BioBench 是一个桌面端的生物序列比对编辑与分析工具，基于 Electron + TypeScript 从零编写。

它的功能设计参考了经典的 BioEdit 序列比对编辑器，目标是用现代界面覆盖 BioEdit 的常用功能。BioBench 是独立实现的程序，不包含 BioEdit 的任何代码、图标或文档，与 BioEdit 及其作者没有关联。

## 功能

| 类别 | 功能 |
| --- | --- |
| 文件 | 读写 FASTA、GenBank（含特征）、EMBL、NBRF/PIR、PHYLIP（交错/顺序）、Clustal、GCG MSF、MEGA、NEXUS、Stockholm、GCG、纯文本；读取 ABI / SCF 色谱图；拖放打开、最近文件、从剪贴板新建 |
| 比对编辑器 | 画布绘制，支持大比对流畅滚动；选择 / 编辑（插入、改写）/ 滑动三种模式；区块、整行、整列选择；插入删除空位；撤销重做；序列锁定；查找；多种配色（核苷酸、ClustalX、Zappo、Taylor、疏水性）；一致性 / 相似性阴影；参考序列点号显示；一致序列行 |
| 序列 | 反向互补、互补、反向、DNA↔RNA、大小写、去空位；六框翻译、格式化翻译报告、反向翻译；组成与分子量、pI、消光系数；密码子使用（RSCU、GC3、ENC）；ORF 查找；IUPAC / PROSITE / 正则基序搜索；点图；双序列比对（全局、局部、末端免罚） |
| 酶切与引物 | 内置约 150 种商品化限制酶（REBASE）；酶切图谱、虚拟酶切片段、质粒图谱；寡核苷酸 Tm（最近邻法）、分子量、发夹与二聚体 |
| 比对分析 | ClustalW 风格渐进式多序列比对、谱比对、一致序列、一致性矩阵、香农熵、互信息、位点汇总、保守区、密码子对齐（翻译视图切换） |
| 系统发育 | p、JC69、K2P、F81、Tamura、TN93、LogDet、Poisson、Kimura 蛋白距离；NJ、UPGMA；Bootstrap 与多数规则一致树；树查看器（矩形、斜线、环形、无根）；中点 / 外群定根；Newick 导入导出 |
| RNA | 二级结构预测（最小自由能简化模型、Nussinov）；环形图与弧形图；共变分析 |
| 网络 | NCBI BLAST 在线搜索、Entrez 下载、调用本地 BLAST+ |
| 导出 | SVG / PNG / 文本 / CSV 导出、打印、导出 PDF；浅色 / 深色主题 |

## 开发

需要 Node.js 22 或更高版本。

```bash
npm install
```

```bash
npm start
```

```bash
npm run check
```

`npm run check` 依次运行类型检查、单元测试和打包构建。

## 打包 Windows 程序

```bash
npm run dist
```

生成的便携版程序位于 `release/BioBench-<版本>-portable.exe`，双击即可运行，不需要安装。

## 目录结构

```
src/core/       纯 TypeScript 算法库（无 DOM / Node 依赖，单元测试覆盖）
  io/           文件格式读写
  trace/        ABI / SCF 色谱图
  align/        打分矩阵、双序列比对、多序列比对、比对操作与统计
  analysis/     组成、密码子、ORF、基序、点图、限制酶、引物、蛋白、RNA
  phylo/        距离模型、建树、Bootstrap、Newick、树布局
  plasmid/      质粒图谱布局
  web/          NCBI BLAST / Entrez / 本地 BLAST+
src/main/       Electron 主进程
src/preload/    预加载脚本（window.biobenchHost）
src/renderer/   界面：编辑器、菜单、对话框、结果视图
test/core/      单元测试
```

## 数据来源

- 打分矩阵：NCBI BLAST 矩阵、ClustalW 2.1
- 遗传密码：NCBI genetic codes
- 限制酶：REBASE
- 最近邻热力学参数：SantaLucia (1998)
