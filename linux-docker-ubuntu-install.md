---
title: Ubuntu 安装 Docker Engine
copyright: BY-NC-ND
date: 2023-03-02 22:32:31
tags:
    - Linux
    - Ubuntu
    - Docker
    - from-repo-mine
---

- [1. 清理旧版本](#1-清理旧版本)
- [2. 安装方法](#2-安装方法)
- [3. 方法一 从仓库安装](#3-方法一-从仓库安装)
  - [3.1. 建立仓库](#31-建立仓库)
    - [3.1.1. 更新 `apt` 包索引，并安装相关依赖](#311-更新-apt-包索引并安装相关依赖)
    - [3.1.2. 添加 Docker 官方 GPG 公钥](#312-添加-docker-官方-gpg-公钥)
    - [3.1.3. 建立仓库（stable）](#313-建立仓库stable)
  - [3.2. 安装 Docker Engine](#32-安装-docker-engine)
    - [3.2.1. 安装最新版本的 Docker Engine](#321-安装最新版本的-docker-engine)
    - [3.2.2. 安装特定版本的 Docker Engine](#322-安装特定版本的-docker-engine)
- [4. 方法二 从软件包安装](#4-方法二-从软件包安装)
  - [4.1. 下载 .deb 软件包](#41-下载-deb-软件包)
  - [4.2. 安装 Docker Engine](#42-安装-docker-engine)
- [5. 启动 Docker 服务](#5-启动-docker-服务)
- [6. 测试 Docker Engine](#6-测试-docker-engine)

> 【参考】Install Docker Engine on Ubuntu | Docker Documentation: <https://docs.docker.com/engine/install/ubuntu/>
>
> 【参考】Docker CE 镜像源站-阿里云开发者社区  <https://developer.aliyun.com/article/110806>
> 【规范】模仿 Docker 文档，Ubuntu, Docker 首字母都采用大写。
>
> 【环境】
>
> 阿里云 ecs.t5-lc2m1.nano ubuntu_20_04_x64_20G_alibase_20210521.vhd

## 1. 清理旧版本

```shell
sudo apt remove docker docker-engine docker.io containerd runc
```

## 2. 安装方法

1. 方法一：【推荐】适合联网安装
   1. 建立 Docker 仓库
   2. 从 Docker 仓库安装或更新
2. 方法二：适合离线安装
   1. 下载 DEB 软件包
   2. 手动安装或更新

## 3. 方法一 从仓库安装

### 3.1. 建立仓库

#### 3.1.1. 更新 `apt` 包索引，并安装相关依赖

```shell
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release
```

#### 3.1.2. 添加 Docker 官方 GPG 公钥

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

#### 3.1.3. 建立仓库（stable）

```shell
# 可以在 stable 参数后添加 nightly 或 test
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 3.2. 安装 Docker Engine

以下方法二选一

#### 3.2.1. 安装最新版本的 Docker Engine

```shell
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

#### 3.2.2. 安装特定版本的 Docker Engine

1. 列举仓库中可用的版本

    ```shell
    apt-cache madison docker-ce
    ```

   - 返回示例

    ```shell
    docker-ce | 5:20.10.7~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.6~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.5~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.4~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.3~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.2~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    docker-ce | 5:20.10.1~3-0~ubuntu-focal | https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
    ```

2. 从第二列中选择并安装特定的版本

    ```shell
    sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
    ```

- 以 `5:20.10.7~3-0~ubuntu-focal` 为例

    ```shell
    sudo apt install docker-ce=5:20.10.7~3-0~ubuntu-focal docker-ce-cli=5:20.10.7~3-0~ubuntu-focal containerd.io
    ```

## 4. 方法二 从软件包安装

### 4.1. 下载 .deb 软件包

前往 <https://download.docker.com/linux/ubuntu/dists/> 根据需求选择 Ubuntu 版本后进入 `\pool` 目录，选择 Docker Engine 的版本（[Ubuntu 发行版名称对照列表](./[Ubuntu]%20发行版列表.md)）

- e.g.

    ```shell
    wget https://download.docker.com/linux/ubuntu/dists/focal/pool/stable/amd64/containerd.io_1.4.6-1_amd64.deb
    wget https://download.docker.com/linux/ubuntu/dists/focal/pool/stable/amd64/docker-ce-cli_20.10.7~3-0~ubuntu-focal_amd64.deb
    wget https://download.docker.com/linux/ubuntu/dists/focal/pool/stable/amd64/docker-ce_20.10.7~3-0~ubuntu-focal_amd64.deb
    ```

### 4.2. 安装 Docker Engine

```shell
sudo dpkg -i [软件包的存储位置]
```

- e.g.

    ```shell
    # 需顺序安装
    sudo dpkg -i containerd.io_1.4.6-1_amd64.deb
    sudo dpkg -i docker-ce-cli_20.10.7~3-0~ubuntu-focal_amd64.deb
    sudo dpkg -i docker-ce_20.10.7~3-0~ubuntu-focal_amd64.deb
    ```

## 5. 启动 Docker 服务

```shell
sudo systemctl start docker
systemctl status docker

# wsl2 中可以使用
sudo service docker start
service docker status
```

## 6. 测试 Docker Engine

```shell
sudo docker run hello-world
```

若返回一段相关信息并退出，则 Docker Engine 安装正常

```shell
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

> 【扩展】GPG入门教程 - 阮一峰的网络日志: <http://www.ruanyifeng.com/blog/2013/07/gpg.html>

<!--
Copyright © 2022, 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->