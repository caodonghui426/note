比赛地址：https://www.kaggle.com/competitions/blood-vessel-segmentation

# 1. Overview

本次比赛的目标是分割血管。您将创建一个模型，该模型经过训练使用来自人类肾脏的3D分层相位对比断层扫描（HiP-CT）数据，以帮助完整地呈现出全身血管系统的图像。您的工作将有助于研究人员更好地理解人体组织中血管的大小、形状、分支角度和图案。

## 1.1 描述

您身体的器官和组织依赖于细胞之间的相互作用、空间组织和专门化，而这些细胞总共有370万亿个。研究人员通过血管通用坐标框架（VCCF）来理解细胞功能和关系。VCCF使用人体内的血管系统作为主要导航系统来映射细胞。该框架跨越所有尺度级别，并提供了一种独特的方式，可以使用毛细血管结构作为地址来确定细胞位置。然而，研究人员对于血管系统所知甚少，这也导致了VCCF中存在缺口。如果数据科学能够帮助自动分割血管排列，研究人员就可以利用真实世界的组织数据填补这些缺口，并完善他们对全身血管系统的认识。

目前，人类专家标注员手动追踪血管结构，这是一个缓慢的过程。即使有专家标注员的帮助，每个新数据集也需要6个月以上才能完成。使用这些手动数据进行机器学习方法在新数据集上泛化效果不佳，因为人体解剖结构和HiP-CT技术不断改进和变化导致图像质量存在差异。

竞赛主办方共同基金的细胞衰老网络（SenNet）计划旨在全面识别和描述身体各部位、人类健康状况以及寿命不同状态下的衰老细胞之间的差异。SenNet提供公开可访问的衰老细胞图谱，并开发建立在单细胞分析先前进展基础上的创新工具和技术。

SenNet在这次比赛中与人体器官图谱（HOA）合作。HOA是一个数字图谱，包含3D多分辨率成像数据集，是在世界上最亮的同步加速器（欧洲同步辐射设施）上创建的，使用了一种称为分层相位对比断层摄影术（HiP-CT）的成像技术。HiP-CT跨越了研究者对人体解剖学理解中以前未被充分探索的尺度范围，从微米到完整无损的器官。

您的努力可以改善我们对血管系统对人体不同细胞的影响的理解。有了更好的数据，研究人员可以模拟血液、氧气甚至药物在血管网络中的流动。他们还可以利用现有器官图像来增强对性别、年龄和BMI变化时血管系统变化的理解。最终，您可以帮助铺平通向更完整的Vascular Common Coordinate Framework（VCCF）和Human Reference Atlas（HRA）之路，这将能够确定细胞间关系如何影响我们的健康。

## 1.2 评测

我们使用表面Dice指标进行评估，容差为0.0。

您可以在这个笔记本中找到该指标的代码：表面Dice指标。

## 1.3 提交文件

对于测试集中的每个`id`，您必须预测`rle`，即一种以运行长度编码的实例分割掩模。其中`id`表示具有路径`test/{dataset}/images/{slice}.tif`的图像的`{dataset}_{slice}`。将空掩模的RLE表示为`1 0`.

您提交的内容应包含标题，并具有以下格式：

```bash
id,rle
kidney_5_0,1 1 100 10
kidney_5_1,1 1 100 10
kidney_6_0,1 0
kidney_6_1,1 0
...
```

## 1.4 时间线

- **November 7, 2023** - Start Date.
- **January 30, 2024** - Entry Deadline. You must accept the competition rules before this date in order to compete.
- **January 30, 2024** - Team Merger Deadline. This is the last day participants may join or merge teams.
- **February 6, 2024** - Final Submission Deadline.

除非另有说明，所有截止日期均为当天UTC时间晚上11:59。比赛组织者保留根据需要更新竞赛时间表的权利。

## 1.5 代码要求

**This is a Code Competition**

参赛作品必须通过笔记本提交。为了在提交后激活“提交”按钮，必须满足以下条件：

- CPU Notebook <= 9 hours run-time
- GPU Notebook <= 9 hours run-time
- Internet access disabled
- Freely & publicly available external data is allowed, including pre-trained models
- Submission file must be named `submission.csv`

请查看“代码竞赛常见问题解答”以获取更多关于如何提交的信息。如果您遇到提交错误，请参阅代码调试文档。