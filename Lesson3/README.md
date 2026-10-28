# 第三课 · 激活函数、梯度与训练稳定性

[返回项目首页](../README.md)

本课练习包括激活函数及其导数、宽网络与深网络、梯度消失与爆炸，以及 BatchNorm、残差连接和梯度裁剪。

## 练习入口

| 练习 | 内容 | 入口 |
| :--- | :--- | :--- |
| Practice 1 | 实现 Sigmoid、Tanh、ReLU 及其导数，观察饱和区与死区 | [Notebook](practice1/Practice%201%20Activation%20Functions%20in%20Code.ipynb) · [结果图](practice1/activation_23.png) |
| Practice 2 | 使用 CIFAR10 子集，对比宽网络和深网络的参数量与训练损失 | [Notebook](practice2/Practice%202%20Wide%20vs%20Deep%20Networks.ipynb) |
| Practice 3 | 对比 Sigmoid/ReLU 的各层梯度，观察权重放大的影响 | [Notebook](practice3/Practice%203%20Gradient%20Vanishing%20and%20Explosion.ipynb) |
| Practice 4 | 测量 BatchNorm、残差连接与全局梯度范数裁剪的影响 | [Notebook](practice4/Practice%204%20Normalization%20and%20Residual%20Connections.ipynb) |

## 运行方式

先按[项目首页](../README.md#快速开始)安装依赖，选择对应的 Python 内核，按题目要求设置 `SID`，从上到下运行 Notebook。

运行时以对应的 `practice` 目录为工作目录。例如，在项目根目录运行：

```bash
cd Lesson3/practice3
python -m notebook
```

## 数据准备

Practice 1 使用 Notebook 内生成的数值，无需下载数据集。Practice 2、3、4 共用一份 CIFAR10 数据。

所有 `data/` 目录均已加入 `.gitignore`，克隆项目后需自行下载数据；本地已有的完整缓存可继续使用。

### CIFAR10 · Practice 2 / Practice 3 / Practice 4

[数据集官网](https://www.cs.toronto.edu/~kriz/cifar.html) · [TorchVision 文档](https://docs.pytorch.org/vision/stable/generated/torchvision.datasets.CIFAR10.html)

**自动下载（推荐）**

在项目根目录、已安装 `torchvision` 的 Python 环境中运行：

```bash
python -c "from torchvision.datasets import CIFAR10; CIFAR10(root='Lesson3/practice2/data', train=True, download=True)"
```

该命令会下载并解压数据，下载量约为 170 MB；完整缓存已存在时不会重复下载。

**手动下载**

从数据集官网选择 **CIFAR-10 python version**，下载 `cifar-10-python.tar.gz`，解压后将 `cifar-10-batches-py` 文件夹放到下面的位置：

```text
Lesson3/practice2/data/cifar-10-batches-py/
├── batches.meta
├── data_batch_1
├── data_batch_2
├── data_batch_3
├── data_batch_4
├── data_batch_5
└── test_batch
```

### 数据路径与复用

| 练习 | 工作目录（相对项目根目录） | Notebook 中的 `DATA_ROOT` |
| :--- | :--- | :--- |
| Practice 2 | `Lesson3/practice2/` | `"data"` |
| Practice 3 | `Lesson3/practice3/` | `"../practice2/data"` |
| Practice 4 | `Lesson3/practice4/` | `"../practice2/data"` |

三个练习最终都读取 `Lesson3/practice2/data/` 下的数据。缓存完整时，Practice 3、4 无需再次下载；缓存目录不存在时，Notebook 会自动下载。

- Practice 2 使用 3,000 条训练样本，对两个网络进行训练。
- Practice 3、4 使用一个 256 条样本的批次，仅进行前向与反向传播，不执行训练更新。

> Notebook 的缓存判断只检查数据文件夹是否存在。如果文件缺失或下载中断，请补齐数据；仅有空文件夹无法正常加载。

## 输出与路径

Practice 1 将图片保存为 `activation_<SID>.png`；Practice 2 将训练曲线保存为 `wide_vs_deep_<SID>.png`。这些图片保存到当前工作目录。

Practice 3、4 主要输出各层梯度范数及比较结果。在编辑器中可运行 `import os; print(os.getcwd())` 确认工作目录。
