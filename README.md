# 数据集说明

本项目包含两组公开的解混数据集：`gf5` 和 `zh1`。两组数据集具有类似的结构，均包含高光谱数据、丰度结果以及端元束结果。以下将详细说明各个文件夹以及文件的含义。

---

## 顶层文件夹

- **gf5**  
  表示高分五号数据集。
- **zh1**  
  表示珠海一号数据集。

gf5和zh1文件夹结构及其内容一致，以下以 `gf5` 为例详细说明。

---

## gf5 文件夹结构说明

### 根目录

- **gf5.npy**  
  表示 GF5 高光谱图像数据，数据格式为 `.npy`，可使用 `numpy` 读取。

- **abundance_result_gf5**  
  表示gf5.npy的丰度结果，详见下文中对该文件夹的详细说明。

- **EndMember_Bundle**  
  表示端元束结果。

---

### abundance_result_gf5 文件夹

该文件夹包含基于不同分析方法生成的丰度结果，主要分为三种类型：

1. **abundance_result_H_MESMA**  
   - 丰度结果由基于分层的多端元光谱混合分析(H_MESMA)得到。
   - 丰度矩阵结果存储为 `.npy`文件，尺寸为(N,H*W)，其中：N为端元数量，H 和 W 分别为图像的高和宽。
     - 丰度矩阵按端元顺序代表的地物类别为["water", "tree", "soil", "grass", "roof", "road"]
   - 每个端元的丰度结果存储为 `.png` 图像。例如：
     - `端元1丰度图.png`
     - `端元2丰度图.png`
     - ...

2. **abundance_result_seg**  
   - 表示采用高分辨图像协同得到的丰度结果。
   - **特点**：不包含分割结果含背景的像元的丰度值。
   - 丰度矩阵结果存储为 `.npy`文件，尺寸为(H,W,N),其中：H 和 W 分别为图像的高和宽，N为端元数量。
     - 端元按顺序代表的地物类别为["water", "tree", "soil", "grass", "roof", "road"]
   - 每个端元的丰度结果存储为 `.png` 图像。例如：
     - `端元1丰度图.png`
     - `端元2丰度图.png`
     - ...

3. **abundance_result_C_CA**  
   - 表示高分辨率图像协同得到的丰度结果。
   - **特点**：分割结果中含背景的像元的丰度值由H_MESMA得到。
   - 丰度矩阵结果存储为 `.npy`文件，尺寸为(H,W,N),其中：H 和 W 分别为图像的高和宽，N为端元数量。
     - 端元按顺序代表的地物类别为["water", "tree", "soil", "grass", "roof", "road"]
   - 每个端元的丰度结果存储为 `.png` 图像。例如：
     - `端元1丰度图.png`
     - `端元2丰度图.png`
     - ...


---

## ZH1 文件夹结构说明

ZH1 数据集的文件夹结构与 GF5 数据集完全一致，各文件的含义相同。ZH1 文件夹包含：

- **zh1.npy**  
  存储珠海一号高光谱图像数据。

- **abundance_result_zh1**  
  存储丰度结果，可分为以下三类：
  1. `abundance_result_H_MESMA`
  2. `abundance_result_seg`
  3. `abundance_result_C_CA`

- **End_Member_Bundle**  
  存储端元束结果。

---

---

## 其他

- **如何加载 `.npy` 文件**  
  通过以下代码可以加载 `.npy` 格式的文件：

  ```python
  import numpy as np
  abundance = np.load('路径/to/abundance.npy')
  print(abundance.shape)  # 输出矩阵形状
