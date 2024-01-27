---
title: 更换 cnetos 软件源
copyright: BY-NC-ND
date: 2023-10-08 18:35
tags:
    - Linux
    - centos
---

# linux-centos-mirror

> 实践环境: CentOS Linux release 7.8.2003 (Core)

## 1. 备份软件源目录

```shell

sudo cp -r /etc/yum.repos.d/ /etc/yum.repos.d.bk

```

## 2. 修改软件源列表

运行一下命令，修改软件源

- CentOS 7

```shell

sudo sed -e 's|^mirrorlist=|#mirrorlist=|g' \

         -e 's|^#baseurl=http://mirror.centos.org|baseurl=https://mirrors.tuna.tsinghua.edu.cn|g' \

         -i.bak \

         /etc/yum.repos.d/CentOS-*.repo

```

- CentOS 8

```shell

sudo sed -e 's|^mirrorlist=|#mirrorlist=|g' \

         -e 's|^#baseurl=http://mirror.centos.org/$contentdir|baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos|g' \

         -i.bak \

         /etc/yum.repos.d/CentOS-*.repo

```

## 更新软件包缓存

```shell

sudo yum makecache

```

## 参考

1. centos | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror: <https://mirrors.tuna.tsinghua.edu.cn/help/centos/>
2. CentOS 源使用帮助 — USTC Mirror Help 文档: <https://mirrors.ustc.edu.cn/help/centos.html>

## 感谢

感谢 清华大学镜像站，南京大学镜像站提供镜像服务

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->
