---
title: Latex 安装
copyright: BY-NC-ND
date: 2023-05-28 22:16:42
tags:
    - software
    - latex
    - from-mine
categories:
    - software
---

## 1. 安装 Tex Live

> - 操作环境：windows 10/11
> - 【参考】<https://tug.org/texlive/acquire-netinstall.html>

1. Tex Live : <http://tug.org/texlive/>
2. CTAN : <https://www.ctan.org/>
3. proTeXt - a TeX distribution for Windows : <http://www.tug.org/protext/>
4. SumatraPDF reader : <https://github.com/sumatrapdfreader/sumatrapdf>

### 1.1. 离线安装 Tex Live（使用 iso）

1. 前往 <https://www.ctan.org/mirrors> 挑选合适的镜像源（比较纠结的话，就选择离自己比较近的即可）
   1. 我这儿选择了阿里云镜像源：<https://mirrors.aliyun.com/CTAN/systems/texlive/Images/>
2. 在镜像站内，选择下载合适的 Tex Live iso 文件，如 texlive.iso <https://mirrors.aliyun.com/CTAN/systems/texlive/Images/texlive.iso>
3. 打开 `texlive.iso` 运行 `install-tl-windows.bat` (若给全体用户安装，需要手动选择管理员模式)
4. 按照安装程序的提示，配置 Tex Live 安装位置等参数
5. 等待安装程序执行（耗时相当久，约两小时，有大量的小文件）
6. `latex -version` 命令检查是否配置正确

### 1.2. 在线安装 Tex Live

1. 下载 `install-tl-windows.exe` <https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe>
2. 运行 install-tl-windows.exe (若给全体用户安装，需要手动选择管理员模式)
   1. 或解压 install-tl.zip 运行 install-tl-windows.bat
3. 在弹出的 install-tl-gui 窗口中，迅速选择镜像源（窗口只呈现较短时间）
   1. 未选择则将使用默认镜像源（网速较慢）
   2. 此处选择阿里云镜像站 CTAN 镜像源 <https://mirrors.aliyun.com/CTAN/>

   ![选择CTAN镜像源](https://raw.githubusercontent.com/cc01cc/zeorep/main/pic/202210091935684.png)
4. 按照安装程序的提示，配置 Tex Live 安装位置等参数
5. 等待安装程序执行（耗时相当久，网络正常约4个小时，有大量的小文件，我安装的时候有4千多个）
6. `latex -version` 检查是否配置正确（否则需要手动配置环境变量）

### 1.3. 安装检验

```shell
tex -v
```

### 1.4. 后期修改 Tex Live 镜像源

> - 【参考】<https://developer.aliyun.com/mirror/CTAN>
> - 此处使用阿里云镜像站 CTAN 镜像源

临时切换，可以用如下命令：

```shell
# update --all 参数可根据需要修改
tlmgr update --all --repository https://mirrors.aliyun.com/CTAN/systems/texlive/tlnet
```

长期更换，可以使用如下命令：

```shell
tlmgr option repository https://mirrors.aliyun.com/CTAN/systems/texlive/tlnet
```

<!--
Copyright © 2023 [github.com/cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->