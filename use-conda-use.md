---
title: Conda 使用指南
copyright: BY-NC-ND
date: 2023-03-11 23:22:46
tags:
categories:
    - python
---

> <https://conda.io/projects/conda/en/latest/index.html>

- 环境： `conda/4.12.0 requests/2.25.1 CPython/3.8.* Windows/10 Windows/10.0.19041`
- 由于编辑顺序的差异，`mamba` 和 `conda` 命令存在混用的情况，未安装 `mamba` 的读者可以使用 `conda` 平替大部分 `mamba` 命令。

- [1. 快速开始](#1-快速开始)
- [2. 阅读资料](#2-阅读资料)
- [3. 使用 mamba 提速 conda](#3-使用-mamba-提速-conda)
- [4. 在 anaconda 中使用 pip 的相关建议](#4-在-anaconda-中使用-pip-的相关建议)
- [5. 更新 conda](#5-更新-conda)
- [6. 管理环境](#6-管理环境)
  - [6.1. 使用命令行创建环境](#61-使用命令行创建环境)
  - [6.2. 安装环境到指定目录](#62-安装环境到指定目录)
  - [6.3. 配置创建环境时的默认包](#63-配置创建环境时的默认包)
  - [6.4. 查看环境](#64-查看环境)
  - [6.5. 克隆环境](#65-克隆环境)
  - [6.6. 删除环境](#66-删除环境)
  - [6.7. 导出环境](#67-导出环境)
  - [6.8. 导入环境](#68-导入环境)
  - [6.9. 向 jupyter notebook 中添加 kernel](#69-向-jupyter-notebook-中添加-kernel)
  - [6.10. 从 requirements.txt 文件创建环境](#610-从-requirementstxt-文件创建环境)
  - [6.11. 从 environment.yml 文件创建环境](#611-从-environmentyml-文件创建环境)
  - [6.12. 其他环境创建参数](#612-其他环境创建参数)
  - [6.13. 常用命令](#613-常用命令)
- [7. 包处理](#7-包处理)
  - [7.1. 删除没有用的包](#71-删除没有用的包)
  - [7.2. 移除指定包](#72-移除指定包)
  - [7.3. 附](#73-附)
- [8. 扩展操作](#8-扩展操作)

## 1. 快速开始

```shell
conda create -n  demo-38 python=3.8
conda activate demo-38
conda update --all
conda install ipykernel pandas seaborn -c anaconda -c conda-forge
python -m  ipykernel install --user --name demo-38 --display-name demo-38-kernel
```

## 2. 阅读资料

1. Anaconda | For Practitioners: <https://www.anaconda.com/blog/topic/for-practitioners>

<https://www.tensorflow.org/install/pip#windows-native>

## 3. 使用 mamba 提速 conda

[[use-conda-mamba]] 使用 mamba 提速 Conda - 零一居: <https://cc01cc.com/2022/11/15/use-conda-mamba/>

## 4. 在 anaconda 中使用 pip 的相关建议

> - Managing environments — conda documentation: <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#using-pip-in-an-environment>
> - Anaconda | Using Pip in a Conda Environment: <https://www.anaconda.com/blog/using-pip-in-a-conda-environment>

简而言之，conda 无法识别 pip 安装的库，会导致 conda 重复安装 pip 安装过的库，基于此，建议：

- 只在 conda 之后使用 pip
  - 使用 conda 安装尽可能多的需求，然后使用 pip。
  - pip 应该使用 `——upgrade-strategy only-if-needed` 运行(即默认值)。
  - pip 不使用 `——user` 参数，避免所有用户安装。
- 使用 conda 环境进行隔离
  - 创建一个 conda 环境来隔离 pip 所做的任何更改。
  - 由于硬链接，环境占用的空间很少。
  - 应该注意避免在根环境中运行 pip。（避免安装给所有环境）
- 如果需要更改，则重新创建环境
  - 一旦使用了 pip, conda 将不知道这些更改。
  - 要安装额外的 conda 包，推荐重新创建环境。
- 将 conda 和 pip 需求存储在文本文件中
  - 包需求可以通过 `——file` 参数传递给 `conda` 。
  - pip 接受带有 `-r` 或 `——requirements` 的 `Python` 包列表
  - `conda env` 将根据包含 `Conda` 和 `pip` 需求的文件导出或创建环境。

## 5. 更新 conda

```shell
# 更新 conda
conda update -n base -c defaults conda
# 查看 conda 版本
conda --version
```

## 6. 管理环境

> <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>

### 6.1. 使用命令行创建环境

```shell
# 创建环境
conda create -n zeoenv
# 指定 python 环境
conda create -n zeoenv python=3.8
# 指定环境所需的包
conda create -n zeoenv numpy scipy ipykernel
# conda 中常用的环境
conda create -n demo-38 python=3.8 scipy matplotlib scikit-learn ipykernel pandas seaborn notebook -c conda-forge -c anaconda
```

### 6.2. 安装环境到指定目录

conda create -p /your_path/env_name

### 6.3. 配置创建环境时的默认包

- 默认包在每次创建环境会自动添加，使用命令行参数 `--no-default-packages` 阻止
- 在配置文件 `.condarc`，`create_default_packages:` 参数内添加环境的默认包，

### 6.4. 查看环境

- 使用 `conda env list` 或 `conda info --envs` 查看环境
- 当前环境使用 `*` （星号）突出标记
- 查看环境中的包列表 `conda list -n zeoenv`

### 6.5. 克隆环境

使用 `conda create -n zeoclone --clone zeoenv` 克隆环境

### 6.6. 删除环境

使用 `conda remove -n zeoenv --all` 删除环境

### 6.7. 导出环境

> Managing environments — conda documentation: <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-the-environment-yml-file>

```shell
# 导出所有库
conda env export > environment.yml
# 导出明确指定的库（不包含版本号，使用 .condarc 中的 channels）
conda env export --from-history > environement.yml
# 手动添加 channel
conda env export > environment-from-history.yml --from-history -c defaults -c conda-forge -c anaconda -c intel
```

### 6.8. 导入环境

> Managing environments — conda documentation: <https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file>

`conda env create --file output.yaml`

### 6.9. 向 jupyter notebook 中添加 kernel

1. `conda install ipykernel`
2. 将环境写入notebook的kernel中 `python -m ipykernel install --user --name 环境名称 --display-name 内核名字`

### 6.10. 从 requirements.txt 文件创建环境

`conda install --file requirements.txt -c default -c conda-forge`

### 6.11. 从 environment.yml 文件创建环境

1. 创建环境 `conda env create -f environment.yml`
2. 激活环境 `conda activate zeoenv` （环境的名称在 yml 文件的第一行）
3. 更新环境 `conda env update -f enivironment.yml --prue`

### 6.12. 其他环境创建参数

1. 指定环境位置
   1. 参数：`--prefix ./subEnvs`
   2. 环境激活：`conda activate ./subEnvs`

### 6.13. 常用命令

```shell
# 自动检测并升级 Anaconda 管理器中的所有可升级的库
conda update --all
# 激活环境
conda activate zeoenv
# 离开环境
conda deactivate zeoenv
# 查看指定环境的历史版本
conda list -n env_name --revision
# 回退到指定环境的版本
conda install --revision 0
```

## 7. 包处理

### 7.1. 删除没有用的包

`conda clean -p`

### 7.2. 移除指定包

> - Conda uninstall package - Askavy: <https://askavy.com/conda-uninstall-package/>
> - conda remove — conda 22.9.0.post32+14f95c41f documentation: <https://docs.conda.io/projects/conda/en/latest/commands/remove.html>

```shell
# 移除制定包及其依赖
conda remove 包名 [-n 环境名]
```

### 7.3. 附

1. 【扩展】Anaconda | Understanding Conda and Pip: <https://www.anaconda.com/blog/understanding-conda-and-pip>
2. 【参考】pip install 和conda install有什么区别吗？ - ZERO-XJ的回答 - 知乎
<https://www.zhihu.com/question/395145313/answer/2551141843>

## 8. 扩展操作

> Troubleshooting — Anaconda documentation : <https://docs.anaconda.com/anaconda/user-guide/troubleshooting/>

```shell
# 查看 info
conda info
```

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->