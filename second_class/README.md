# 第二课 · 神经网络训练基础

[返回项目首页](../README.md)

本课练习包括前向传播、二元交叉熵、数值梯度、计算图反向传播和梯度下降可视化。

## 练习入口

| 练习 | 内容 | 入口 |
| :--- | :--- | :--- |
| Practice 1 | 用 NumPy 实现两层全连接网络的前向计算 | [Notebook](practice1/Practice1.ipynb) |
| Practice 2 | 实现二元交叉熵与平均代价，并生成演示图 | [Notebook](practice2/Practice2.ipynb) · [结果图](practice2/bce_demo.png) |
| Practice 3 | 实现数值梯度与计算图反向传播，生成梯度下降动画 | [Notebook](practice3/Practice3.ipynb) · [动画](practice3/gradient_descent.gif) |

## 运行方式

先按[项目首页](../README.md#快速开始)安装依赖，选择对应的 Python 内核，从上到下运行 Notebook。绘图和 GIF 输出使用 NumPy、Matplotlib 和 Pillow。

运行时以对应的 `practice` 目录为工作目录。例如，在项目根目录运行：

```bash
cd second_class/practice3
python -m notebook
```

## 数据准备

本课的三个练习均使用 Notebook 内构造的数据，无需下载 MNIST、CIFAR10 或其他外部数据集。

## 输出与路径

- Practice 2 将演示图保存为 `bce_demo.png`。
- Practice 3 将梯度下降动画保存为 `gradient_descent.gif`，生成 GIF 需要一些时间。

这些输出使用相对路径，保存到当前工作目录。在编辑器中可运行 `import os; print(os.getcwd())`，确认工作目录为对应练习目录。
