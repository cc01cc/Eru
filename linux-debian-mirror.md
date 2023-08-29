---
title: 更换 Debian 软件源
copyright: BY-NC-ND
date: 2023-03-17 14:01:00
tags:
    - Linux
    - Debian
---

## 运行以下命令备份软件源并配置镜像源

```shwll
sudo sed -e 's|^deb http://deb.debian.org/|deb https://mirror.nju.edu.cn/|g' \
         -i.bak \
         /etc/apt/sources.list
```

## 感谢

感谢 NJU Mirror 提供的镜像服务 Help - NJU Mirror <https://mirrors.nju.edu.cn/>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->