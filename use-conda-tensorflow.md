---
title: 安装 tensorflow GPU（使用 conda）
date: 2022-12-06
tags:
    - Python
    - Conda
    - from-repo-mine
categories:
    - python
---

> 环境：windows 11

## 1. 快速开始

运行以下命令，直接新建一个包含 tensorflow (gpu) 以及其他常用库的新环境。

```shell
# 采用下方「方法二」创建一个包含 tensorflow 与常用包的环境
conda create -n tensorflow-38 python=3.8.13 matplotlib scikit-learn ipykernel pandas seaborn tensorflow-gpu -c conda-forge -c anaconda
conda activate tensorflow-38
# pip install opencv-python
```

## 2. 「方法一」半自动安装

- 先安装 cudnn 和 cudatoolkit 包，再安装 tensorflow 包

```shell
conda create -n tensorflow-38-1 python=3.8.13
conda activate tensorflow-38-1

# 会自动安装 cudatoolkit
conda install -c conda-forge cudnn
pip install tensorflow
```

## 3. 「方法二」全自动安装

- 缺点是版本相对 pypi 稍低
- 如：目前 pypi 版本为 2.8，conda 的版本为 2.6
- `conda install tensorflow-gpu` 和 `pip install tensorflow-gpu` 安装的内容是不同的

```shell
conda create -n tensorflow-38-2 python=3.8.13
conda activate tensorflow-38-2

# conda-forge channel 的 tensorflow-gpu 仅支持 Linux
conda install tensorflow-gpu -c anaconda
```

## 4. 验证

```python
import tensorflow as tf
# 查看 tensorflow 版本
print(tf.__version__)
# 判断是否使用 GPU 构建
print(tf.test.is_built_with_cuda())
# 查看GPU列表
print(tf.config.list_physical_devices('GPU'))
# 查看驱动名称
if tf.test.gpu_device_name():
    print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
else:
    print("Please install GPU version of TF")
```

## 5. 提示

在后期修改环境的时候，留意不要把 `tensorflow-gpu` 从 gpu 版本换成 cpu 版本，如下图所示：

![tensorflow 降级](https://raw.githubusercontent.com/cc01cc/zeorep/main/pic/202211102218460.png)

## 6. 附

- 「参考」TensorFlow — Anaconda documentation: <https://docs.anaconda.com/anaconda/user-guide/tasks/tensorflow/>
- 「扩展」Anaconda | TensorFlow in Anaconda: <https://www.anaconda.com/blog/tensorflow-in-anaconda>

- 不太清楚 `conda install -c nvidia cuda` 命令的作用，因为网络问题，一直没有成功过（也没有找到合适的镜像源）

<!--
Copyright © 2022,2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc/cc01cc>
-->