<div align="center">

# OUC Deep Learning

深度学习课程的学习笔记、实践代码与实验记录

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

[课程内容](#课程内容) · [快速开始](#快速开始) · [数据准备](#数据准备)

</div>

本仓库按课程章节整理 Notebook、示例图片和实验结果，随学习进度持续更新。目前收录第一课、第二课和第三课 Practice 1–4。

## 课程内容

### 第一课 · 基础实践

| 练习 | 主题 | 内容 | 入口 |
| :--- | :--- | :--- | :---: |
| Practice 1 | Notebook 入门 | 函数、随机数与基础绘图 | [Notebook](first_class/practice1/Practice1.ipynb) |
| Practice 2 | 数据拟合 | 对比直线、多项式与小型神经网络的拟合结果和损失 | [Notebook](first_class/practice2/Practice2.ipynb) |
| Practice 3 | 数据加载 | MNIST、Dataset、DataLoader 与批次 | [Notebook](first_class/practice3/Practice3.ipynb) |
| Practice 4 | 图像分类 | 使用预训练 ResNet18 进行推理，查看 Top-5 预测 | [Notebook](first_class/practice4/练习4.ipynb) |

### 第二课 · 神经网络训练基础

| 练习 | 主题 | 内容 | 入口 |
| :--- | :--- | :--- | :---: |
| Practice 1 | 前向传播 | 用 NumPy 实现两层全连接网络的前向计算 | [Notebook](second_class/practice1/Practice1.ipynb) |
| Practice 2 | 损失函数 | 实现二元交叉熵与平均代价，并生成演示图 | [Notebook](second_class/practice2/Practice2.ipynb) · [结果图](second_class/practice2/bce_demo.png) |
| Practice 3 | 梯度与反向传播 | 实现数值梯度与计算图反向传播，生成梯度下降动画 | [Notebook](second_class/practice3/Practice3.ipynb) · [动画](second_class/practice3/gradient_descent.gif) |

<p align="center">
  <img src="second_class/practice3/gradient_descent.gif" alt="梯度下降轨迹可视化" width="620">
  <br>
  <sub>第二课 Practice 3 · 梯度下降轨迹</sub>
</p>

### 第三课 · 激活函数、梯度与训练稳定性

| 练习 | 主题 | 内容 | 状态 | 入口 |
| :--- | :--- | :--- | :--- | :---: |
| Practice 1 | 激活函数 | 实现 Sigmoid、Tanh、ReLU 及其导数，观察饱和区与死区 | 已填写，已有结果图 | [Notebook](third_class/practice1/Practice%201%20Activation%20Functions%20in%20Code.ipynb) · [结果图](third_class/practice1/activation_23.png) |
| Practice 2 | 宽网络与深网络 | 使用 CIFAR10 子集，对比参数量与训练损失曲线 | 已填写，待完整训练验证 | [Notebook](third_class/practice2/Practice%202%20Wide%20vs%20Deep%20Networks.ipynb) |
| Practice 3 | 梯度消失与爆炸 | 测量各层梯度范数，对比 Sigmoid/ReLU，并观察权重放大的影响 | 已填写并运行验证 | [Notebook](third_class/practice3/Practice%203%20Gradient%20Vanishing%20and%20Explosion.ipynb) |
| Practice 4 | 归一化与残差连接 | 对比 BatchNorm、残差连接对梯度的影响，并验证全局梯度范数裁剪 | 已填写并运行验证 | [Notebook](third_class/practice4/Practice%204%20Normalization%20and%20Residual%20Connections.ipynb) |

Practice 3 在 `SID=42`、8 个隐藏层、每层 64 个单元的设置下，测得首层/末层梯度比例：Sigmoid 约为 `1.163e-6`，ReLU 约为 `4.573e-2`。将权重乘以 8 后，首层梯度范数约为 `1.153e5`，显著增大但仍为有限值，没有出现 `inf` 或 `nan`。

Practice 4 在 `SID=42` 的设置下，首层梯度范数分别为：基线 `5.652e-7`、加入 BatchNorm 后 `1.119`、残差网络 `0.631`。裁剪前总梯度范数约为 `0.317`，低于阈值 `0.5`，因此保持不变；额外验证确认超出阈值时，裁剪能限制全局范数并保留梯度方向。以上均为单批次梯度测量，不代表完整训练后的性能。

## 快速开始

### 1. 获取项目

```bash
git clone https://github.com/yuanfendtiankong/Ouc_DeepLearning.git
cd Ouc_DeepLearning
```

### 2. 安装依赖

在你使用的 Python 环境中安装 Jupyter Notebook 和通用依赖：

```bash
python -m pip install notebook numpy matplotlib pillow
```

另外，根据操作系统及 CPU/CUDA 环境，按照 [PyTorch 官方安装指南](https://docs.pytorch.org/get-started/locally/)安装兼容的 `torch` 和 `torchvision`。

### 3. 打开 Notebook

```bash
jupyter notebook
```

打开对应练习的 `.ipynb` 文件，选择已安装依赖的 Python 内核，从上到下运行。按题目要求设置 `SID`。第一课 Practice 3 需要先完成下方的 MNIST 数据准备。

部分 Notebook 使用 `data`、图片文件名等相对路径，运行时应以对应的 `practice` 目录为工作目录。例如，从项目根目录启动第三课 Practice 3：

```bash
cd third_class/practice3
python -m notebook
```

在 VS Code 等编辑器中，可用 `import os; print(os.getcwd())` 确认内核的工作目录。生成的图片也会保存到当前工作目录。

## 数据准备

所有 `data/` 数据目录均已加入 `.gitignore`，不会随仓库提交。克隆项目后，请按下面的说明下载数据；本地已有的完整缓存可以继续使用。

第二课的三个练习使用 Notebook 内构造的数据，当前无需额外下载数据集。

### MNIST · 第一课 Practice 3

[数据集官网](https://yann.lecun.org/exdb/mnist/index.html) · [TorchVision 文档](https://docs.pytorch.org/vision/stable/generated/torchvision.datasets.MNIST.html)

**自动下载（推荐）**

在项目根目录运行一次，TorchVision 会下载并解压所需文件：

```bash
python -c "from torchvision.datasets import MNIST; MNIST(root='first_class/practice3/data', download=True)"
```

数据将保存在 `first_class/practice3/data/MNIST/raw/`。该数据目录已加入 `.gitignore`，克隆仓库后需自行下载。

> 第一课 Practice 3 使用 `root="./data"`，运行时应以 `first_class/practice3/` 为工作目录。完成上述下载后，可保留 Notebook 中的 `download=False`。

<details>
<summary>手动下载：文件链接与目录结构</summary>

以下是 TorchVision 使用的 MNIST 镜像文件：

| 内容 | 下载链接 |
| :--- | :--- |
| 训练图像 | [train-images-idx3-ubyte.gz](https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz) |
| 训练标签 | [train-labels-idx1-ubyte.gz](https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz) |
| 测试图像 | [t10k-images-idx3-ubyte.gz](https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz) |
| 测试标签 | [t10k-labels-idx1-ubyte.gz](https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz) |

下载后解压四个 `.gz` 文件，确保以下不带 `.gz` 后缀的文件存在：

```text
first_class/practice3/data/MNIST/raw/
├── train-images-idx3-ubyte
├── train-labels-idx1-ubyte
├── t10k-images-idx3-ubyte
└── t10k-labels-idx1-ubyte
```

</details>

### CIFAR10 · 第三课 Practice 2 / Practice 3 / Practice 4

[数据集官网](https://www.cs.toronto.edu/~kriz/cifar.html) · [TorchVision 文档](https://docs.pytorch.org/vision/stable/generated/torchvision.datasets.CIFAR10.html)

Practice 2 使用 `DATA_ROOT = "data"`，读取其练习目录下的 `data/cifar-10-batches-py/`；Practice 3 和 Practice 4 使用 `DATA_ROOT = "../practice2/data"`，复用同一份缓存。未在指定路径找到数据文件夹时会自动下载，下载量约为 170 MB。

**自动下载（推荐）**

在项目根目录、已安装 `torchvision` 的 Python 环境中运行：

```bash
python -c "from torchvision.datasets import CIFAR10; CIFAR10(root='third_class/practice2/data', train=True, download=True)"
```

该命令会下载并解压数据；完整缓存已存在时不会重复下载。Practice 2、3、4 共用这一份数据即可。

**手动下载**

从数据集官网选择 **CIFAR-10 python version**，下载 `cifar-10-python.tar.gz`，解压两层压缩包后，将 `cifar-10-batches-py` 文件夹放到下面的位置。请使用 Python 版本，不要选择 Matlab 或 binary 版本。

```text
third_class/practice2/data/cifar-10-batches-py/
├── batches.meta
├── data_batch_1
├── data_batch_2
├── data_batch_3
├── data_batch_4
├── data_batch_5
└── test_batch
```

- Practice 2 使用 3,000 条训练样本，对宽网络与深网络进行训练。
- Practice 3 使用一个 256 条样本的批次，仅进行前向与反向传播，不执行训练更新。
- Practice 4 同样使用一个 256 条样本的批次，测量归一化、残差连接与梯度裁剪的影响。

运行时应分别以 `third_class/practice2/`、`third_class/practice3/` 或 `third_class/practice4/` 为工作目录，确保上述相对路径能正确定位数据。Practice 2 的缓存完整时，Practice 3 和 Practice 4 无需再次下载。

> 缓存判断只检查数据文件夹是否存在。如果文件缺失或下载中断，需补齐数据后再运行；仅有空文件夹无法正常加载。

### 图片输入 · 第一课 Practice 4

Notebook 默认读取同目录下的 `my_photo.jpg`。使用其他图片时，将图片放入练习目录，并修改 `IMG_PATH` 指向对应文件。
