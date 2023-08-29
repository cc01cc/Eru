---
title: 更换 Ubuntu 软件源
copyright: BY-NC-ND
date: 2023-03-17 14:01:00
tags:
    - Linux
    - Ubuntu
    - from-repo-mine
---

> 【环境】Ubuntu: 20.04 LTS

## 1. 备份默认软件源列表

```shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

## 2. 修改软件源列表

### [方法一] 命令修改配置文件

```shell
sudo sed -e 's|^deb http://archive.ubuntu.com/|deb https://mirror.nju.edu.cn/|g' \
         -e 's|^# deb-src http://archive.ubuntu.com/|# deb-src https://mirror.nju.edu.cn/|g' \
         -i.bak \
         /etc/apt/sources.list
```

### [方法二] 手动修改配置文件

> 使用 `vi` 命令，因为大部分 Linux 都自带了这个编辑器，不需要更新
>
> *（vim，VS Code 以及 SSH 远程连接都需要下载或更新相关软件）*

1. 使用 `sudo vi /etc/apt/sources.list` 打开软件源配置文件
2. 使用 `ggdG` 删除已有内容
3. 复制下方镜像链接（注意版本），右键（或 `p`）粘贴到配置文件中
4. 使用 `:wq` 保存并退出

*当没有使用 `sudo` 提升权限，导致无法退出时，可以使用 `:qa!` 退出

具体地址可以访问各大镜像站
例：[https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

* 20.04 LTS 版本

```txt
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

* 18.04 LTS 版本

```txt
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

## 参考

1. 怎么修改ubuntu的软件源 - 问答 - 亿速云 : <https://www.yisu.com/ask/5735.html>
2. ubuntu | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror: <https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/>
3. Help - NJU Mirror <https://mirrors.nju.edu.cn/help/ubuntu>

## 感谢

感谢 清华大学镜像站，南京大学镜像站提供镜像服务

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->