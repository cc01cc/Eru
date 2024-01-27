---
title: Ubuntu 安装 Todesk
copyright: BY-NC-ND
date: 2023-03-01 22:55:17
tags:
    - Ubuntu
---

> 环境：Ubuntu 22.04 LTS

## 1. 更新软件源

```shell
sudo apt update
```

## 2. 安装 x11

Ubuntu 22.04 默认使用 Wayland 图形系统，但是 Todesk 仅支持 x11

> 1. Debian11 与ubuntu22.04做被控端无法显示桌面 - Bug 反馈 - Powered by Discuz! <https://bbs.todesk.com/thread-2457-1-1.html>
> 2. software installation - How to install X11/xorg? - Ask Ubuntu <https://askubuntu.com/questions/213678/how-to-install-x11-xorg>

```shell
sudo apt-get install xorg openbox
```

## 3. 使用 x11

> 1. Configuring Xorg as the default GNOME session :: Fedora Docs <https://docs.fedoraproject.org/en-US/quick-docs/configuring-xorg-as-default-gnome-session/>

注销用户 > 登录界面（点击用户后，输入密码的界面）> 单击右下角有个齿轮 > 在弹窗中选择 Xorg

## 4. 下载并安装 Todesk

> Linux - ToDesk <https://todesk.com/linux.html>

1. 下载安装包：安装包地址可以访问 <https://todesk.com/linux.html> > 左侧列表选择 Ubuntu
2. 进入下载目录，一般默认下载目录在 `~/Download`
3. 使用 `sudo apt install ./todesk-**-**.deb` 安装 Todesk

## 5. 运行 Todesk

使用 `todesk` 命令运行 Todesk

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc/cc01cc>
-->