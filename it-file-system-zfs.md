---
title: 初识 zfs
copyright: BY-NC-ND
date: 2023-04-11 16:06:21
tags:
    - TODO
    - 待校验
    - new-bing
    - zfs
    - file system
---

## 1. 定义

- **ZFS**：ZFS 是一种先进的文件系统和逻辑卷管理器，它提供了数据完整性保护、高存储容量、快照和写时复制克隆等功能。
- **存储池**：存储池是 ZFS 结构的最上层。一个存储池包含一个或多个虚拟设备（vdev），每个虚拟设备又包含一个或多个设备。存储池是独立的单元，一台物理计算机上可能有两个或更多个独立的存储池，但每个存储池都是完全独立的。存储池之间不能共享虚拟设备。

## 2. 创建方法

### 2.1. Ubuntu

> 环境：Ubuntu 系统
>
> zpool | Ubuntu Manpage: <https://manpages.ubuntu.com/manpages/focal/man8/zpool.8.html>

```bash
# 安装 ZFS 软件包
sudo apt install zfsutils-linux

# 创建新的 ZFS 存储池
sudo zpool create pool_name vdev1 vdev2 ...

# 查看存储池状态
sudo zpool status pool_name
```

## 3. 管理方法

### 3.1. 添加和删除设备

```bash
# 向存储池添加虚拟设备
sudo zpool add pool_name vdev

# 替换故障磁盘
sudo zpool replace pool_name failed_disk new_disk
```

## 参考资料

- [ZFS - Wikipedia](https://en.wikipedia.org/wiki/ZFS)
- [ZFS on Linux - Ubuntu Wiki](https://wiki.ubuntu.com/ZFS)

## 扩展资料

- openzfs/zfs: OpenZFS on Linux and FreeBSD: <https://github.com/openzfs/zfs>
- Getting Started — OpenZFS documentation: <https://openzfs.github.io/openzfs-docs/Getting%20Started/index.html>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本文部分内容改编自与 Microsoft Bing 的对话

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->