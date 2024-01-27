---
title: apt 与 apt-get 的区别
copyright: BY-NC-ND
date: 2023-04-30 18:59:24
tags:
    - from-mine
    - linux
categories:
    - linux
---

> 【参考】 Difference Between apt and apt-get Explained - It's FOSS : <https://itsfoss.com/apt-vs-apt-get-difference/>

## 简述

1. `apt-get`, `apt-cache` 相对于 `apt` 命令相对低级，拥有大量相似的命令与不常用的功能；
2. `apt` 是 `apt-get` 和 `apt-cache` 的子集，提供相对常用的命令。

## 细节差异

> 【参考】apt(8) — apt — Debian jessie — Debian Manpages : <https://manpages.debian.org/jessie/apt/apt.8.en.html>

1. 优化终端用户体验
    e.g. 在默认配置下，**apt** `install` / `remove` 会显示进度条；在 `upgrade` / `update` 会显示软件包的数量。
2. 命令差异
    |apt command|the command it replaces
    |--|--|
    |apt install|apt-get install|
    |apt remove|apt-get remove|
    |apt update|apt-get update|
    |apt upgrade|apt-get upgrade|
    |apt *full-upgrade*|apt-get *dist-upgrade*|
    |apt search|apt-cache search|
    |apt show|apt-cache show|
3. `apt` 限定命令
   |new apt command|function of the command|
   |--|--|
   |apt list|Display a list of package|
   |apt edit-sources|Edits sources list|

> 【扩展】apt.conf(5): config file for APT - Linux man page : <https://linux.die.net/man/5/apt.conf>
> 【扩展】Aptitude - Debian Wiki : <https://wiki.debian.org/Aptitude>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->