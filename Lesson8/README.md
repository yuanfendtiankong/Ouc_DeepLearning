# 第八课 · 目标检测与点积注意力

[返回项目首页](../README.md)

本课从滑动窗口与检测损失入手，练习边界框变换、IoU 和检测指标，再实现点积注意力和 RPN 锚框标签分配，最后按题设计算 R-CNN 和 YOLO 分类头的参数量。

## 练习入口

| 练习 | 内容 | 入口 |
| :--- | :--- | :--- |
| Practice 1 | 滑动窗口候选框计数与多任务检测损失 | [Notebook](practice1/Practice1.ipynb) |
| Practice 2 | 批量边界框变换、交并比（IoU）、Precision 和 Recall | [Notebook](practice2/Practice2.ipynb) |
| Practice 3 | 点积注意力、RPN 锚框标签与分类头参数量 | [Notebook](practice3/Practice3.ipynb) |

## 实现要点

| 练习 | 函数 | 计算说明 |
| :--- | :--- | :--- |
| Practice 1 | `count_sliding_windows` | 分别计算高和宽方向上连续区间的数量，再将两者相乘。用整数除法得到候选框总数。 |
| Practice 1 | `compute_multitask_loss` | 对预测框和真实框的四个坐标求平方误差和，乘上 `reg_weight` 后加到分类损失上。 |
| Practice 2 | `apply_bbox_transform` | 输入是两组形状为 `(N, 4)` 的数组。用候选框的宽高缩放中心偏移，用 `exp` 缩放宽高，返回形状为 `(N, 4)` 的新框。 |
| Practice 2 | `calculate_iou` | 输入框格式为 `[x1, y1, x2, y2]`。用交集面积除以并集面积，无重叠或并集面积为零时返回 `0.0`。 |
| Practice 2 | `calculate_metrics` | 分别用 `TP / (TP + FP)` 和 `TP / (TP + FN)` 计算 Precision 与 Recall；分母为零时，对应指标返回 `0.0`。 |
| Practice 3 | `dot_product_attention` | 计算 query 与各个 key 的点积，减去最大分数后做 softmax，再对 value 加权求和。 |
| Practice 3 | `assign_anchor_labels` | 最大 IoU 小于 `0.3` 时标为 `0`，大于或等于 `0.7` 时标为 `1`，其余标为 `-1`（忽略）。 |
| Practice 3 | `compare_heads` | 按题设计算 R-CNN 的 `N * (D * C + C)`，以及 YOLO 的 `D * (S * S * C) + S * S * C`。 |

Practice 2 的批量变换使用中心坐标与宽高 `[x, y, w, h]`。如需对变换后的框计算 IoU，先将它转换为两个角点的坐标。

## 运行方式

按[项目首页](../README.md#快速开始)配置环境，打开对应的 Notebook，选择已安装 NumPy 的 Python 内核，从上到下运行。三项练习可独立运行，无需准备数据集或预训练权重。

八道题的代码均已补全，保留了题目原有的注释与自动评分单元格。当前 Notebook 中没有保存示例输出或评分结果。
