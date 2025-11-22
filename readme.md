# 📚 1. 数据集说明

## 1.1 数据集总览

数据集主目录位于：`wiper\ReID_Dataset`

该目录包含多个子数据集，每个子数据集对应一种特定的预处理方法或图像分辨率。

## 1.2 数据子集结构

以下是 `wiper\ReID_Dataset` 目录下关键的 CSI 图像数据集及其说明：

| 数据集名称 | 描述 | 预处理方法 | 分辨率 |
| :--- | :--- | :--- | :--- |
| **`image_wiper`** | **论文提供图片数据** | **IQR处理** | $496 \times 369$ |
| **`image_raw`** | **原始csi未经预处理** | **无预处理** | $52 \times 100$ |
| **`image_HF`** | **原始csi用HF** | **HF预处理** | $52 \times 100$ |
| **`image_zscore`** | **原始csi用zscore** | **zscore预处理** | $52 \times 100$ |
| **`image_IQR`** | **原始csi用IQR** | **IQR预处理** | $52 \times 100$ |

在**`image_IQR`**数据集上进行上采样：
| 数据集名称 | 上采样方法 | 上采样倍数 | 分辨率 |
| :--- | :--- | :--- | :--- |
| **`ImageData_gs_UP2`** | **高斯超分** | ×2 | $104 \times 200$ |
| **`ImageData_gs_UP3`** | **高斯超分** | ×3 | $156 \times 300$ |
| **`ImageData_gs_UP4`** | **高斯超分** | ×4 | $208 \times 400$ |
| **`ImageData_bilinear_UP2`** | **双线性插值** | ×2 | $104 \times 200$ |
| **`ImageData_bilinear_UP3`** | **双线性插值** | ×3 | $156 \times 300$ |
| **`ImageData_bilinear_UP4`** | **双线性插值** | ×4 | $208 \times 400$ |

为了生成上述上采样数据集，需要运行以下相应的 Python 脚本：

* **高斯超分 (GS\_UP)**
    * **运行文件：** `GSASR-master\TrainTestGSASR\wifi_process.py`
    * **说明：** 用于将图像通过训练好的高斯超分模型放大。

* **双线性插值 (Bilinear)**
    * **运行文件：** `bilinear_upsampler.py`
    * **说明：** 简单的双线性插值操作。
---
# 📚 2.数据可视化文件说明

#### 📁 文件夹：`DFSExtractionCode`

该文件夹包含了用于生成**幅度曲线图**和**动态频率谱 (DFS) 图**的 Python 脚本。

## 2.1 幅度曲线图绘制

* **脚本名称：** `amplitude_curves.py`
* **核心功能：** 绘制 CSI 幅度叠加曲线图。
* **描述：** 每条曲线代表一个时间帧，用于直观观察信道幅度在短时间内的波动和频率选择性。
* **举例：**<img width="778" height="569" alt="image" src="https://github.com/user-attachments/assets/2e3ab50e-4081-4ce3-8462-beb6e98952e1" />

## 2.2 动态频率谱 (DFS) 图绘制

##### a) 核心逻辑转换文件（ Widar 3.0）

这些文件包含了从 Widar 3.0 提供的的 MATLAB 代码转换而来的 Python 核心处理逻辑：

* `generate_vs.py`
* `get_doppler_spectrum.py`

##### b) WiPER 数据集 DFS 图生成

这些脚本是针对 WiPER 数据集的 DFS 图生成工具：

* **`generate_vs_csv`**
    * **功能：** 绘制完整 DFS 图。
    * **描述：** 针对 WiPER 数据集中的**整个 CSV 文件**，生成一张完整的动态频率谱图。
* **举例：** <img width="746" height="466" alt="image" src="https://github.com/user-attachments/assets/77166ec4-943f-42b5-9202-f55e1e4cfdfb" />

* **`generate_vs_csv_split`**
    * **功能：** 绘制分段 DFS 图。
    * **描述：** 将输入的 CSV 文件数据**划分为 10 份**，并分别绘制 10 张 DFS 图，对应于 $100 \times 52$ 尺寸的热图。
* **举例：** <img width="526" height="312" alt="image" src="https://github.com/user-attachments/assets/5bc4fb24-ab6e-4424-8cfb-c5605cdce9e7" />

* **`get_doppler_spectrum_csv_split.py`**
    * **描述：** 包含了 `generate_vs_csv` 和 `generate_vs_csv_split` 脚本所依赖的底层 DFS 谱计算和数据处理逻辑。

