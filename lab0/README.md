# Lab 0：在本地训练第一个图像分类模型

- [lab0_local.ipynb](lab0_local.ipynb)：中文本地版，按顺序运行即可。默认用少量真实 CIFAR-10 图片练习整个流程。
- [lab0.ipynb](lab0.ipynb)：MIT 6.5940 原版 Colab 笔记本，保留作对照。

## 在这台 Windows 电脑上开始

1. 用 VS Code 打开 `Course-TinyML` 文件夹，再打开 `lab0/lab0_local.ipynb`。
2. 点右上角 **选择内核（Select Kernel）→ Python 环境（Python Environments）**，选择 `lab0\.venv\Scripts\python.exe`。列表里找不到时，在 VS Code 命令面板用 **Python: Select Interpreter** 手动输入这个路径，再回笔记本选内核。
3. 读完一格再按 **Shift+Enter** 运行它。第一次建议保持 `mode = "quick"`，先看懂一批图片怎样变成预测结果。

笔记本会打印实际使用的 Python、CPU/GPU 和数据目录。CIFAR-10 首次需要下载约 163 MiB，解压后保存在 `lab0/data/cifar10`，以后会复用。快速模式也会下载完整数据包，只在训练和评估时抽取一部分。

## 换电脑或需要重建环境时

在项目根目录打开 PowerShell，使用 Python 3.13。下面的命令安装 CPU 版 PyTorch，无需管理员权限，也无需激活虚拟环境：

```powershell
cd .\lab0
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

VS Code 需要 **Python** 和 **Jupyter** 扩展。若改用浏览器里的 JupyterLab，在同一目录运行：

```powershell
.\.venv\Scripts\python.exe -m pip install jupyterlab
.\.venv\Scripts\python.exe -m jupyterlab
```

| 模式 | 数据与训练设置 | 适合做什么 |
| --- | --- | --- |
| `"quick"`（默认） | 2,048 张训练图、1,000 张测试图；较窄的 VGG，3 轮 | 先学会读形状、看损失和检查预测 |
| `"course"` | 50,000 张训练图、10,000 张测试图；原版 VGG，20 轮 | 体验原课配置；建议使用 NVIDIA GPU |

改配置后，重启内核并从头运行。如果要在新环境中用 NVIDIA GPU，在 [PyTorch 官方安装选择器](https://pytorch.org/get-started/locally/) 选 Windows、Pip 和适用的 CUDA 版本，用生成的命令替换上面安装 CPU 版的那一行。把命令开头的 `pip` 或 `pip3` 换成 `.\.venv\Scripts\python.exe -m pip`。笔记本检测到 CUDA 可用时会自动选 GPU。

如果提示找不到包，先检查右上角内核是否选对。若 CPU 训练太慢，可以先把快速模式的 `num_epochs` 改成 1。第一次学习时，能解释「训练如何改变模型的预测」比追求课件里的准确率更有用。

如果首次下载失败，可以从 [CIFAR-10 官方数据页面](https://www.cs.toronto.edu/~kriz/cifar.html) 下载 **CIFAR-10 python version**，把 `cifar-10-python.tar.gz` 放到 `lab0/data/cifar10`，然后重跑数据格。笔记本会校验和解压它。
