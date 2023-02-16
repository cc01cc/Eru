---
title: 使用 mamba 提速 conda
# description: 
date: 2022-11-16
slug: conda-mamba-20221116
categories:
    - python
tag:
    - python
    - conda
---

> 安装 mamba 耗时较久，推荐刚安装 anaconda 时直接安装 mamba。

## 介绍

> GitHub - mamba-org/mamba: The Fast Cross-Platform Package Manager: <https://github.com/mamba-org/mamba>

mamba 是 conda 包管理器的 C++ 重新实现

- 使用多线程并行下载存储库数据和包文件
- 使用 libsolv 加速处理依赖关系
- 为了提高效率，mamba 的核心部分使用 c++ 实现的
- 为了提高兼容性，mamba 使用与 conda 相同的命令行解析器、包安装和卸载代码以及事务验证例程。（即 mamba 和 conda 用法几乎相同）

## 安装

> Installation — documentation: <https://mamba.readthedocs.io/en/latest/installation.html>

1. 运行 `conda activate -n base` 进入 `base` 环境
2. 运行 `conda install mamba -n base -c conda-forge` 安装 `mamba`

## 使用

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

## 参考

1. Anaconda | Understanding and Improving Conda's performance: <https://www.anaconda.com/blog/understanding-and-improving-condas-performance>

---

- 署名：cc01cc: <https://github.com/cc01cc>
- 欢迎大家转载分享，本作品采用[署名-非商业性使用-禁止演绎 4.0 国际](https://creativecommons.org/licenses/by-nc-nd/4.0/)进行许可，转载请标明源地址，切莫修改或破坏原文结构，谢谢
