---
title: 使用 mamba 提速 Conda
date: 2022-11-16
tags:
    - Python
    - Conda
    - from-repo-mine
categories:
    - python
---

## 1. 介绍

> GitHub - mamba-org/mamba: The Fast Cross-Platform Package Manager: <https://github.com/mamba-org/mamba>

mamba 是 Conda 包管理器的 C++ 重新实现

- 使用多线程并行下载存储库数据和包文件
- 使用 libsolv 加速处理依赖关系
- 为了提高效率，mamba 的核心部分使用 C++ 实现的
- 为了提高兼容性，mamba 使用与 Conda 相同的命令行解析器、包安装和卸载代码以及事务验证例程。（即 mamba 和 Conda 用法几乎相同）

## 2. 安装

下载安装包，安装包地址：

GitHub - conda-forge/miniforge: A conda-forge distribution. <https://github.com/conda-forge/miniforge#mambaforge>

- Windows 系统 双击 exe 文件
- Linux Mac 系统 运行 `bash Mambaforge-$(uname)-$(uname -m).sh` 命令即可
  - 请根据实际，调整文件名称

### 2.1. [已不推荐]安装

> 安装 mamba 耗时较久，推荐刚安装 anaconda 时直接安装 mamba。
>
> Installation — documentation: <https://mamba.readthedocs.io/en/latest/installation.html>

1. 运行 `conda activate base` 进入 `base` 环境
2. 运行 `conda install mamba -n base -c conda-forge` 安装 `mamba`

## 3. 使用

除了 `activate`, `deactivate` 外，`mamba` 使用和 `conda` 相同的命令和配置，例如

```bash
mamba install ...
mamba create -n ... -c ... ...
mamba list
conda activate ...
```

如果需要更加快速的查询库可以使用 `mamba repoquery` 命令

```bash
# will show you all available xtensor packages.
$ mamba repoquery search xtensor

# you can also specify more constraints on this search query
$ mamba repoquery search "xtensor>=0.18"

# will show you a list of the dependencies of xtensor.
$ mamba repoquery depends -t xtensor
```

## 4. 参考

1. Anaconda | Understanding and Improving Conda's performance: <https://www.anaconda.com/blog/understanding-and-improving-condas-performance>

<!--
Copyright © 2022,2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc>
-->