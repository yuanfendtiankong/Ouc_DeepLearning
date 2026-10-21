<div align="center">

# OUC Deep Learning

深度学习课程的学习笔记、实践代码与实验记录

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

[课程内容](#课程内容) · [快速开始](#快速开始)

</div>

本仓库按课程章节整理 Notebook、示例图片和实验结果，随学习进度持续更新。目前收录第一至第四课的练习，涵盖神经网络基础、梯度与训练稳定性，以及 CNN、RNN 的结构与前向传播。

## 课程内容

### 第一课 · 基础实践

[课程说明与数据准备](first_class/README.md)

| 练习 | 主题 | 内容 | 入口 |
| :--- | :--- | :--- | :---: |
| Practice 1 | Notebook 入门 | 函数、随机数与基础绘图 | [Notebook](first_class/practice1/Practice1.ipynb) |
| Practice 2 | 数据拟合 | 对比直线、多项式与小型神经网络的拟合结果和损失 | [Notebook](first_class/practice2/Practice2.ipynb) |
| Practice 3 | 数据加载 | MNIST、Dataset、DataLoader 与批次 | [Notebook](first_class/practice3/Practice3.ipynb) |
| Practice 4 | 图像分类 | 使用预训练 ResNet18 进行推理，查看 Top-5 预测 | [Notebook](first_class/practice4/练习4.ipynb) |

### 第二课 · 神经网络训练基础

[课程说明与数据准备](second_class/README.md)

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

[课程说明与数据准备](third_class/README.md)

| 练习 | 主题 | 内容 | 状态 | 入口 |
| :--- | :--- | :--- | :--- | :---: |
| Practice 1 | 激活函数 | 实现 Sigmoid、Tanh、ReLU 及其导数，观察饱和区与死区 | 已填写，已有结果图 | [Notebook](third_class/practice1/Practice%201%20Activation%20Functions%20in%20Code.ipynb) · [结果图](third_class/practice1/activation_23.png) |
| Practice 2 | 宽网络与深网络 | 使用 CIFAR10 子集，对比参数量与训练损失曲线 | 已填写，待完整训练验证 | [Notebook](third_class/practice2/Practice%202%20Wide%20vs%20Deep%20Networks.ipynb) |
| Practice 3 | 梯度消失与爆炸 | 测量各层梯度范数，对比 Sigmoid/ReLU，并观察权重放大的影响 | 已填写并运行验证 | [Notebook](third_class/practice3/Practice%203%20Gradient%20Vanishing%20and%20Explosion.ipynb) |
| Practice 4 | 归一化与残差连接 | 对比 BatchNorm、残差连接对梯度的影响，并验证全局梯度范数裁剪 | 已填写并运行验证 | [Notebook](third_class/practice4/Practice%204%20Normalization%20and%20Residual%20Connections.ipynb) |

Practice 3 在 `SID=42`、8 个隐藏层、每层 64 个单元的设置下，测得首层/末层梯度比例：Sigmoid 约为 `1.163e-6`，ReLU 约为 `4.573e-2`。将权重乘以 8 后，首层梯度范数约为 `1.153e5`，显著增大但仍为有限值，没有出现 `inf` 或 `nan`。

Practice 4 在 `SID=42` 的设置下，首层梯度范数分别为：基线 `5.652e-7`、加入 BatchNorm 后 `1.119`、残差网络 `0.631`。裁剪前总梯度范数约为 `0.317`，低于阈值 `0.5`，因此保持不变；额外验证确认超出阈值时，裁剪能限制全局范数并保留梯度方向。以上均为单批次梯度测量，不代表完整训练后的性能。

### 第四课 · CNN 与 RNN

| 练习 | 主题 | 内容 | 入口 |
| :--- | :--- | :--- | :---: |
| Practice 1 | MLP 与 CNN 基础 | 图像展平、全连接网络参数量、二维 valid 卷积与展平后的像素距离 | [Notebook](fourth_class/practice1/Practice1.ipynb) |
| Practice 2 | CNN 结构与运算 | 感受野、卷积输出尺寸与参数量、LeNet-5 逐层形状及网络维度计算 | [Notebook](fourth_class/practice2/Practice2.ipynb) · [题目配图](fourth_class/practice2/P2-Q4.png) |
| Practice 3 | 归一化与经典网络 | NumPy 实现 BatchNorm、LayerNorm，计算 AlexNet、Inception 输出并实现残差连接 | [Notebook](fourth_class/practice3/Practice3.ipynb) |
| Practice 4 | CNN 与 RNN 前向传播 | NumPy 实现卷积 → ReLU → 最大池化、Many-to-Many RNN 与 Many-to-One 序列二分类 | [Notebook](fourth_class/practice4/Practice4.ipynb) |

第四课以 Python / NumPy 的计算与结构分析为主，无需下载数据集或预训练权重。Practice 4 已完成三题实现并通过前向传播示例验证；Notebook 保留题目和实现代码。

## 快速开始

### 1. 获取项目

```bash
git clone https://github.com/yuanfendtiankong/Ouc_DeepLearning.git
cd Ouc_DeepLearning
```

### 2. 创建 Conda 环境

在 WSL/Linux 终端中进入项目根目录，使用 [environment.yml](environment.yml) 创建 Python 3.11 环境。课程依赖版本记录在 [requirements.txt](requirements.txt) 中：

```bash
conda env create -f environment.yml
conda activate deep_learning
python -m ipykernel install --user --name deep_learning --display-name "Python (deep_learning)"
```

如果环境已经创建，后续使用前运行 `conda activate deep_learning` 即可。

### 3. 打开 Notebook

在已激活的环境中启动 JupyterLab：

```bash
jupyter lab
```

打开对应练习的 `.ipynb` 文件，选择 **Python (deep_learning)** 内核，从上到下运行。如果使用 VS Code，请在 WSL 窗口中打开项目，再选择该内核。

按题目要求设置 `SID`，并按照各课程 README 准备数据、设置工作目录。Notebook 中的数据路径相对于对应练习目录。
