---
title: 更换 Debian 软件源
copyright: BY-NC-ND
date: 2023-03-17 14:01:00
updated: 2023-10-19
tags:
    - Linux
    - Debian
---

# linux-debian-mirror

## 运行以下命令备份软件源并配置镜像源

> 此命令一并更新了「安全更新软件源」，一般而言，为了更及时地获得安全更新，不推荐使用镜像站安全更新软件源，因为镜像站往往有同步延迟。参考 <https://www.debian.org/security/faq.en.html#mirror>
>
> 但实测，使用原始地址非常缓慢，甚至无法连接，所以还是使用了镜像站的安全更新软件源。如果需要使用原始地址，相关配置文档可以参考：<https://mirrors.bfsu.edu.cn/help/debian/>

```bash
sudo sed -e 's|^deb http://deb.debian.org/|deb https://mirrors.bfsu.edu.cn/|g' \
         -i.bak \
         /etc/apt/sources.list
```

## 配置结果

```properties
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.bfsu.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb-src https://mirrors.bfsu.edu.cn/debian/ bookworm main contrib non-free non-free-firmware

deb https://mirrors.bfsu.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src https://mirrors.bfsu.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware

deb https://mirrors.bfsu.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb-src https://mirrors.bfsu.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware

deb https://mirrors.bfsu.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src https://mirrors.bfsu.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware

# deb https://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
# deb-src https://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
```

## 感谢

感谢 北京外国语大学开源软件镜像站 提供的镜像服务

## 参考

- debian | 镜像站使用帮助 | 北京外国语大学开源软件镜像站 | BFSU Open Source Mirror: <https://mirrors.bfsu.edu.cn/help/debian/>
- Debian 软件仓库镜像使用帮助 - MirrorZ Help: <https://mirror.nju.edu.cn/mirrorz-help/debian/>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->
