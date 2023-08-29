---
title: Conda 配置
copyright: BY-NC-ND
date: 2023-03-07 08:07:08
tags:
    - Python
    - Conda
    - from-repo-mine
categories:
    - python
---

## 1. 命令行操作

### 1.1. 查看配置

```shell
conda config --show
```

### 1.2. 修改配置

```shell
conda config --add key value
conda config --remove key value
conda config --set key value
```

## 2. 配置 Conda 镜像环境

> <https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#show-channel-urls-show-channel-urls>

### 2.1. (windows)使用配置文件修改镜像源

- 使用 `conda info` 命令查看 `.condarc` 配置**文件**位置（一般为 $env:userprofile/.condarc）

- 在 PowerShell 中使用 `notepad $env:userprofile/.condarc` 命令，通过记事本打开 `.condarc` （若提示文件不存在，则点击创建）
  - CMD 中可以使用 `notepad %userprofile%/.condarc` 命令

将以下内容填入 `.condarc` 文件中

```text
channels:
  - defaults
show_channel_urls: true
default_channels:
  - http://mirrors.aliyun.com/anaconda/pkgs/main
  - http://mirrors.aliyun.com/anaconda/pkgs/r
  - http://mirrors.aliyun.com/anaconda/pkgs/msys2
custom_channels:
  conda-forge: http://mirrors.aliyun.com/anaconda/cloud
  msys2: http://mirrors.aliyun.com/anaconda/cloud
  bioconda: http://mirrors.aliyun.com/anaconda/cloud
  menpo: http://mirrors.aliyun.com/anaconda/cloud
  pytorch: http://mirrors.aliyun.com/anaconda/cloud
  simpleitk: http://mirrors.aliyun.com/anaconda/cloud
```

> <https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#channel-locations-channels>

- channels 的 defaults 会引用 default_channels 中的 URL
- show_channel_urls 显示下载内容的 URL

#### 2.1.1. 其他镜像站

> anaconda - NJU Mirror <https://mirror.nju.edu.cn/help/anaconda>

```text
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirror.nju.edu.cn/anaconda/pkgs/main
  - https://mirror.nju.edu.cn/anaconda/pkgs/r
  - https://mirror.nju.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirror.nju.edu.cn/anaconda/cloud
  msys2: https://mirror.nju.edu.cn/anaconda/cloud
  bioconda: https://mirror.nju.edu.cn/anaconda/cloud
  menpo: https://mirror.nju.edu.cn/anaconda/cloud
  pytorch: https://mirror.nju.edu.cn/anaconda/cloud
  simpleitk: https://mirror.nju.edu.cn/anaconda/cloud
```

### 2.2. (windows)使用命令行添加镜像源（失败）

失败原因：custom_channels 的值添加失败；custom_channels 下有仍有键值对，为嵌套关系，但 `--add` 只能添加一个 key；尝试空格，引号，冒号，括号，斜杠等没有找到方法可以嵌套添加

```shell
conda config --set show_channel_urls yes

conda config --add default_channels http://mirrors.aliyun.com/anaconda/pkgs/msys2

conda config --add default_channels http://mirrors.aliyun.com/anaconda/pkgs/r

conda config --add default_channels http://mirrors.aliyun.com/anaconda/pkgs/main

# conda config --add custom_channels conda-forge: http://mirrors.aliyun.com/anaconda/cloud
# conda config --add custom_channels msys2: http://mirrors.aliyun.com/anaconda/cloud
# conda config --add custom_channels bioconda: http://mirrors.aliyun.com/anaconda/cloud
# conda config --add custom_channels menpo: http://mirrors.aliyun.com/anaconda/cloud
# conda config --add custom_channels pytorch: http://mirrors.aliyun.com/anaconda/cloud
# conda config --add custom_channels simpleitk: http://mirrors.aliyun.com/anaconda/cloud
```

- 使用 `conda config --remove channels http://mirrors.aliyun.com/anaconda/pkgs/r` 移除相应配置

### 2.3. (linux)使用配置文件修改镜像源

- 使用 `vim ~/.condarc` 编辑镜像配置文件

### 2.4. 清理索引缓存

运行 `conda clean -i` 命令清除索引缓存，确保使用的是镜像站的索引。

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->