---
title: Conda 安装
copyright: BY-NC-ND
date: 2023-03-11 23:17:36
tags:
    - Python
    - Conda
    - from-repo-mine
categories:
    - python
---

## 1. Windows 安装 Anaconda

1. **访问** Anaconda 产品网站 <https://www.anaconda.com/products/distribution>
2. **下载并运行**安装包
3. 根据安装**向导**完成安装程序

## 2. 云服务器安装 Anaconda (以 Ubuntu 20.04 为例)

1. **访问** Anaconda 产品网站 <https://www.anaconda.com/products/distribution>
2. **复制**适合的 Anaconda Installers 安装包下载链接<https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh>
  ![Anaconda Installers](https://raw.githubusercontent.com/cc01cc/zeorep/main/pic/202210091929360.png)
3. 在服务器中输入以下命令**下载** Anaconda Individual Edition 安装包

   ```bash
   wget -P /tmp https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
   ```

4. **校验**文件完整性

   1. 在服务器中输入以下命令校验文件完整性

      ```bash
      sha256sum /tmp/Anaconda3-2022.10-Linux-x86_64.sh
      ```

   2. Anaconda 安装包哈希值列表: <https://docs.anaconda.com/anaconda/install/hashes/lin-3-64/>

5. 输入以下命令**运行**安装脚本

   ```bash
   bash /tmp/Anaconda3-2022.10-Linux-x86_64.sh
   ```

6. 根据安装**向导**，完成安装操作（以全部选择 yes 为例）
7. **运行** `source ~/.bashrc` 重新加载环境变量

### 2.1. 故障排除

> <https://docs.anaconda.com/anaconda/user-guide/troubleshooting/>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->