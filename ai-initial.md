---
title: 初识 机器学习/深度学习
copyright: BY-NC-ND
date: 2023-04-23 22:25:30
tags:
    - from-mine
categories:
    - ai
---


- [1. 参考教程](#1-参考教程)
- [2. 服务器资源](#2-服务器资源)
- [3. 环境配置](#3-环境配置)
  - [3.1. cudnn, CUDA 的区别](#31-cudnn-cuda-的区别)
  - [3.2. 查询 CUDA 版本](#32-查询-cuda-版本)
  - [3.3. 查询版本](#33-查询版本)
- [4. 训练集/验证集/测试集](#4-训练集验证集测试集)
  - [4.1. K 折交叉验证法](#41-k-折交叉验证法)
- [5. 过拟合](#5-过拟合)
- [6. 环境](#6-环境)
- [7. 数据集](#7-数据集)
  - [7.1. 图像标注](#71-图像标注)
- [8. 数据预处理](#8-数据预处理)
- [9. 训练与预测](#9-训练与预测)
- [10. 验证](#10-验证)
- [11. 预测结果导出](#11-预测结果导出)
- [12. 常用函数](#12-常用函数)

## 1. 参考教程

1. 吴恩达老师的深度学习课程：DeepLearning.AI: Start or Advance Your Career in AI: <https://www.deeplearning.ai/>
2. 李宏毅老师的深度学习课程
3. 《deep learning》Deep Learning（花书）: <https://www.deeplearningbook.org/>
   1. 中文版 exacity/deeplearningbook-chinese: <https://github.com/exacity/deeplearningbook-chinese>
4. 周志华老师的《机器学习》（西瓜书）
5. 《动手学深度学习》 — 动手学深度学习 2.0.0-beta0 documentation <https://zh-v2.d2l.ai/index.html>
   <!-- 1. 不太推荐配套的视频，感觉偏理论，不太容易理解。 -->
6. 深度之眼官方账号的个人空间_哔哩哔哩_bilibili: <https://space.bilibili.com/365093772>

## 2. 服务器资源

1. SageMaker Studio Lab <https://studiolab.sagemaker.aws/>

## 3. 环境配置

> NVIDIA cuDNN | NVIDIA Developer : <https://developer.nvidia.com/cudnn>
> CUDA Zone | NVIDIA Developer : <https://developer.nvidia.com/cuda-zone>

### 3.1. cudnn, CUDA 的区别

> 显卡，显卡驱动,nvcc, cuda driver,cudatoolkit,cudnn到底是什么？ - 知乎 : <https://zhuanlan.zhihu.com/p/91334380>

1. cudnn 调用 CUDA 中的工具
2. Pytroch 中包含 cudnn 库

### 3.2. 查询 CUDA 版本

```shell
# Windows Linux 通用
nvcc --version
```

```python
import torch
print(torch.__version__)

print(torch.version.cuda)
print(torch.backends.cudnn.version())
```

### 3.3. 查询版本

```python
# 查询 opencv 版本
import cv2
cv2.__version__
```

## 4. 训练集/验证集/测试集

训练集：训练数据集，用于训练模型
验证集：用于对模型的少量调整(训练过程中多次调用)
测试集：用于评估模型的效果

通常三个数据集的数据量比例为：6:2:2

### 4.1. K 折交叉验证法

## 5. 过拟合

## 6. 环境

```python
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# 查看当前根目录
print(os.path.dirname(os.path.abspath("__file__")))
```

## 7. 数据集

### 7.1. 图像标注

1. labelme
2. [在线] Make Sense : <https://www.makesense.ai/>
   1. 暂未找到标记错误时如何撤销

## 8. 数据预处理

```python
import pandas as pd
    
# Load data
melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
melbourne_data = pd.read_csv(melbourne_file_path) 
# Filter rows with missing values
melbourne_data = melbourne_data.dropna(axis=0)
# Choose target and features
y = melbourne_data.Price
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'BuildingArea', 
                        'YearBuilt', 'Lattitude', 'Longtitude']
X = melbourne_data[melbourne_features]

from sklearn.model_selection import train_test_split

# split data into training and validation data, for both features and target
# The split is based on a random number generator. Supplying a numeric value to
# the random_state argument guarantees we get the same split every time we
# run this script.
train_X, val_X, train_y, val_y = train_test_split(X, y,random_state = 0)
```

## 9. 训练与预测

```python
from sklearn.tree import DecisionTreeRegressor
# Specify Model
iowa_model = DecisionTreeRegressor(random_state=1)
# Fit Model
iowa_model.fit(train_X, train_y)
```

## 10. 验证

```python
# Make validation predictions and calculate mean absolute error
val_predictions = iowa_model.predict(val_X)
val_mae = mean_absolute_error(val_predictions, val_y)
print("Validation MAE when not specifying max_leaf_nodes: {:,.0f}".format(val_mae))
```

## 11. 预测结果导出

```python
output = pd.DataFrame({'Id': test_data.Id, 'SalePrice': test_preds})
output.to_csv('submission.csv', index=False)
```

## 12. 常用函数

```python
# 导入数据

# 读取列标签
data.columns
```

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->