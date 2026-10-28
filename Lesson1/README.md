# 第一课 · 基础实践

[返回项目首页](../README.md)

本课练习包括 Notebook 入门、数据拟合、MNIST 数据加载和预训练图像分类。

## 练习入口

| 练习 | 内容 | 入口 |
| :--- | :--- | :--- |
| Practice 1 | 函数、随机数与基础绘图 | [Notebook](practice1/Practice1.ipynb) |
| Practice 2 | 对比直线、多项式与小型神经网络的拟合结果 | [Notebook](practice2/Practice2.ipynb) |
| Practice 3 | MNIST、Dataset、DataLoader 与批次 | [Notebook](practice3/Practice3.ipynb) |
| Practice 4 | 使用预训练 ResNet18 查看图片的 Top-5 预测 | [Notebook](practice4/练习4.ipynb) |

## 运行方式

先按[项目首页](../README.md#快速开始)安装依赖，选择对应的 Python 内核，按题目要求设置 `SID`，从上到下运行 Notebook。

运行时以对应的 `practice` 目录为工作目录。例如，在项目根目录运行：

```bash
cd Lesson1/practice3
python -m notebook
```

## 数据准备

Practice 1、2 使用 Notebook 内构造的数据，无需额外下载数据集。Practice 3 需要 MNIST，Practice 4 需要图片输入。

所有 `data/` 目录均已加入 `.gitignore`，克隆仓库后需自行下载数据；本地已有的完整缓存可继续使用。

### MNIST · Practice 3

[数据集官网](https://yann.lecun.org/exdb/mnist/index.html) · [TorchVision 文档](https://docs.pytorch.org/vision/stable/generated/torchvision.datasets.MNIST.html)

**自动下载（推荐）**

在项目根目录、已安装 `torchvision` 的 Python 环境中运行：

```bash
python -c "from torchvision.datasets import MNIST; MNIST(root='Lesson1/practice3/data', download=True)"
```

数据将保存在 `Lesson1/practice3/data/MNIST/raw/`。Notebook 使用 `root="./data"` 和 `download=False`，因此应先准备好数据，再以 `Lesson1/practice3/` 为工作目录运行。

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
Lesson1/practice3/data/MNIST/raw/
├── train-images-idx3-ubyte
├── train-labels-idx1-ubyte
├── t10k-images-idx3-ubyte
└── t10k-labels-idx1-ubyte
```

</details>

### 图片输入 · Practice 4

Notebook 默认读取同目录下的 `my_photo.jpg`。使用其他图片时，将图片放入 `Lesson1/practice4/`，并修改 `IMG_PATH` 指向对应文件。首次加载预训练 ResNet18 权重时可能需要联网下载。

## 输出与路径

图片按 Notebook 中的文件名保存到当前工作目录，例如 `warmup_line_<SID>.png`、`fit_curves_<SID>.png`、`one_image_<SID>.png` 和 `top5_<SID>.png`。

在编辑器中可运行 `import os; print(os.getcwd())` 确认工作目录，避免数据或图片路径指向其他位置。
