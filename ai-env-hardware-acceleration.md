---
title: 机器学习环境搭建-硬件优化
copyright: BY-NC-ND
date: 2023-03-11 23:05:13
tags:
    - ML
    - DL
    - AI
    - CPU
    - GPU
    - Intel
    - AMD
    - Nvidia
    - from-repo-mine
categories:
    - ai
---

> 使用 CPU GPU 加速等紧密贴合硬件的库时，务必查看官方文档的硬件要求
>
> 在测试或搭建硬件优化库时，务必备份原环境，以及及时的备份数据

## 1. Intel CPU + Intel GPU

> - Installing Intel® Distribution for Python* and Intel® Performance...: <https://www.intel.com/content/www/us/en/developer/articles/technical/using-intel-distribution-for-python-with-anaconda.html>

```shell
# 添加 intel channel
conda config --add channels intel
# 核心发行版
conda create -n idp intelpython3_core python=3.x -c intel
# 完整发行版
conda create -n idp intelpython3_full python=3.x -c intel
```

## 2. Nvidia GPU

```shell
# 尽量在最初同时安装 cudnn cudatoolkit
# 后期再安装 cudnn 会比较麻烦
# 只安装 cudatoolkit 后期再添加 cudnn 会存在版本匹配等问题
mamba create -n lab-01 python=3.8 cudnn cudatoolkit
```

## 3. Intel CPU

```SHELL
# 一般各大框架都会默认使用 mkl（所以 intel cpu 一般不需要手动调整）
mamba create -n lab-01 python=3.8 mkl
```

## 4. AMD CPU

> BLAS、OpenBLAS、ATLAS、MKL_openblas mkl - CSDN博客: <https://blog.csdn.net/fuhanghang/article/details/122885265>

暂时没有找到针对 AMD CPU 优化的库，ACML 也停止更新了，如果有关于 AMD CPU 的优化需求可以参考下面两篇文章，删除 MKL 限制 或 使用 OpenBLAS

- Daniël de Kok: Intel MKL on AMD Zen: <https://danieldk.eu/Posts/2020-08-31-MKL-Zen.html>
- AMD CPU 做科学计算还香吗？（2022 年 MKL 与 OpenBLAS 的 NumPy 简单测试）: <https://xcel.me/amd-cpu-numpy-mkl-vs-openblas-2022/>

> - Let's Build Everything - AMD GPUOpen: <https://gpuopen.com/>
> - ACML Downloads & Resources - AMD: <https://developer.amd.com/acml-downloads-resources/>
> - Best Processors for Machine Learning <https://www.sabrepc.com/blog/Deep-Learning-and-AI/best-processors-for-machine-learning>

## 5. 参考

- Anaconda | Open Sourcing Anaconda Accelerate: <https://www.anaconda.com/blog/open-sourcing-anaconda-accelerate>
- Anaconda | Getting Started with GPU Computing in Anaconda: <https://www.anaconda.com/blog/getting-started-with-gpu-computing-in-anaconda>
- 关于 scikit-learn-intelex 提速: Anaconda | Scikit-learn Speed-up with Intel and Anaconda: <https://www.anaconda.com/blog/scikit-learn-speed-up-with-intel-and-anaconda>
- Intel® Extension for Scikit-learn*— Intel(R) Extension for Scikit-learn* 2021.5 documentation: <https://intel.github.io/scikit-learn-intelex/>
- 关于 Modin 提速 pandas: Anaconda | Scale your pandas workflow with Modin – no rewrite required: <https://www.anaconda.com/blog/scale-your-pandas-workflow-with-modin>
- Installation — Modin documentation: <https://modin.readthedocs.io/en/latest/getting_started/installation.html>
- Intel® Distribution of Modin: <https://www.intel.com/content/www/us/en/developer/tools/oneapi/distribution-of-modin.html>
- Anaconda | Getting Started with GPU Computing in Anaconda: <https://www.anaconda.com/blog/getting-started-with-gpu-computing-in-anaconda>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->