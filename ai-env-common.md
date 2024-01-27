---
title: 机器学习环境搭建-常用
copyright: BY-NC-ND
date: 2023-03-11 23:15:06
tags:
    - ai
    - ml
    - dl
    - from-repo-mine
categories:
    - ai
---

## 1. tf-models

> Intel CPU + Nvidia GPU

```shell
# 虽然部分包之间相互依赖，但无需担心，conda 会自动处理的
# 不要单次安装过多的库，可能导致安装失败（如超出终端缓存等）
# 注意添加库的顺序 tensorflow-gpu 需要在 cudatoolkit 之前
# （实测：否则下载的 tensorflow-gpu 不支持 gpu）
mamba create -n tf-models-gpu-308 python=3.8 tensorflow-gpu cudnn cudatoolkit -c anaconda -c conda-forge
# 添加一些提供 gpu 加速的库
# keras 已包含在 tensorflow 中，不再安装
# 手动添加 tensorflow-gpu 避免被覆盖
mamba install tensorflow-gpu scikit-learn-intelex numba mkl-devel modin-all matplotlib ipykernel -c anaconda -c conda-forge
# 添加一些常用的库
mamba install scipy matplotlib scikit-learn pandas seaborn notebook -c anaconda -c conda-forge
# 最后使用 pip 添加 tensorflow-model
# tensorflow/models: https://github.com/tensorflow/models
# 未提供 conda 安装方式，故使用 pip
pip3 install tf-models-official
```

## 2. OpenCV-python

```shell
# conda install scipy matplotlib scikit-learn ipykernel pandas seaborn -c conda-forge -c anaconda

# openCV，请在 conda 之后使用 pip
pip install opencv-python
```

## pytorch(含 cuda)

> Start Locally | PyTorch: <https://pytorch.org/get-started/locally/>

```shell
mamba create -n pytorch-309 python=3.9.16
mamba activate pytorch-309
mamba install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia
# 添加一些常用的库
mamba install scipy matplotlib scikit-learn scikit-learn-intelex scikit-image pandas seaborn notebook tqdm
# scikit-learn-intelex 支持所有 x86 架构的 CPU，包括 Intel 和 AMD
# 参考：https://intel.github.io/scikit-learn-intelex/system-requirements.html#for-cpu
python -m ipykernel install --user --name pytorch-309 --display-name pytorch-309-kernel
```

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->