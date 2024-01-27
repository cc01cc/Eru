---
title: Jupyter Notebooks 使用指南
copyright: BY-NC-ND
date: 2023-03-12 00:39:33
tags:
    - Jupyter Notebook
    - from-repo-mine
---

- [1. 参考](#1-参考)
- [2. 安装 Jupyter Notebook](#2-安装-jupyter-notebook)
  - [2.1. 使用 Anaconda 安装](#21-使用-anaconda-安装)
  - [2.2. 使用 pip 安装](#22-使用-pip-安装)
  - [2.3. 在云服务器中使用 Anaconda 安装](#23-在云服务器中使用-anaconda-安装)
- [3. 更换默认目录](#3-更换默认目录)
  - [3.1. 生成 jupyter notebook 配置文件](#31-生成-jupyter-notebook-配置文件)
  - [3.2. 修改配置文件](#32-修改配置文件)
  - [3.3. 修改 jupyter notebook 快捷方式](#33-修改-jupyter-notebook-快捷方式)
  - [3.4. 重新启动 jupyter notebook](#34-重新启动-jupyter-notebook)
- [4. 快捷键](#4-快捷键)
  - [4.1. 命令模式](#41-命令模式)
  - [4.2. 编辑模式](#42-编辑模式)
- [5. 扩展](#5-扩展)
  - [5.1. 扩展推荐](#51-扩展推荐)
- [6. 技巧](#6-技巧)
  - [6.1. 查看功能列表](#61-查看功能列表)
  - [6.2. 添加交互式仪表盘](#62-添加交互式仪表盘)
  - [6.3. 向 jupyter notebook 中添加 kernel](#63-向-jupyter-notebook-中添加-kernel)
  - [6.4. 查看 jupyter notebook 查看 kernel](#64-查看-jupyter-notebook-查看-kernel)
  - [6.5. 删除 jupyter notebook 中的 kernel](#65-删除-jupyter-notebook-中的-kernel)
- [7. 探索](#7-探索)
- [8. 魔法操作符](#8-魔法操作符)

## 1. 参考

1. 始于 Jupyter Notebooks：一份全面的初学者实用指南 : <https://mp.weixin.qq.com/s/fmFTkRiUoIleugtAoKeaQA>
2. Jupyter Notebook Beginner Guide | What is a Jupyter Notebook : <https://www.analyticsvidhya.com/blog/2018/05/starters-guide-jupyter-notebook/>

## 2. 安装 Jupyter Notebook

### 2.1. 使用 Anaconda 安装

1. 下载 Anaconda | Individual Edition : <https://www.anaconda.com/products/individual>
2. 根据安装引导程序安装 Anaconda
3. Anaconda 同时包含了 Python, Jupyter Notebooks 等多项工具

### 2.2. 使用 pip 安装

1. 更新 pip

    ```shell
    # Linux, MacOS
    pip install -U pip setuptools

    # Windows
    python -m pip install -U pip setuptools
    ```

2. 安装 Jupyter Notebook

    ```shell
    # Python2
    pip install jupyter

    # Python3
    pip3 install jupyter
    ```

### 2.3. 在云服务器中使用 Anaconda 安装

1. 使用如下命令安装 Jupyter Notebook

    ```shell
    conda install jupyter notebook
    ```

2. 给 Jupyter Notebook 设置密码（方法一）
   1. 输入 `python` 命令
   2. 输入以下命令设置密码

        ```python
        >>> from notebook.auth import passwd
        >>> passwd()
        # 按照提示输入密码
        # 保存生成的一串密码哈希值
        ```

   3. 输入 `exit()` 命令退出 Python

3. 给 Jupyter Notebook 设置密码（方法二）
   1. 输入以下命令设置密码

      ```shell
      jupyter notebook password
      ```

   2. 进入生成的文件 `jupyter_notebook_config.json`，复制生成的密码哈希值

4. 配置 Jupyter Notebook
   1. 运行 `jupyter notebook --generate-config` 命令生成配置文件
   2. 进入配置文件配置

    ```text
    c.NotebookApp.allow_origin = '*'
    c.NotebookApp.allow_remote_access = True
    c.NotebookApp.certfile = '/home/ubuntu/.jupyter/xxx.pem' # 这里是 pem 证书文件的路径
    c.NotebookApp.ip = '*'
    c.NotebookApp.keyfile = '/home/ubuntu/.jupyter/xxx.key' # 这里是 key 文件的路径
    c.NotebookApp.notebook_dir = '/home/ubuntu/jupyter-notebook' # 这里是你想让 Jupyter 放项目的文件夹
    c.NotebookApp.password = 'xxxxxx' #之前复制到密码哈希值
    c.NotebookApp.open_browser = False
    c.NotebookApp.port = 8888 # Jupyter 的端口
    ```

## 3. 更换默认目录

### 3.1. 生成 jupyter notebook 配置文件

使用 `CMD/Powershell` 输入 `jupyter notebook --generate-config` 命令，生成配置文件并返回配置文件**地址**（后续要用）。

- 若 `CMD/Powershell` 无法识别 `jupyter notebook`，可以从 `ANACONDA` 内的 `CMD.exe Prompt/Powershell Prompt` 进入。

### 3.2. 修改配置文件

1. 通过上一步骤返回的文件位置，打开配置文件
2. 查找 `# c.NotebookApp.notebook_dir = ''` 参数
3. 在 `''` 内添加自定义的目录
4. 删除注释符 `#` 以及**空格**（python 缩进规范）

### 3.3. 修改 jupyter notebook 快捷方式

1. 进入快捷方式属性
2. 在**目标**栏，`"%USERPROFILE%/"` 参数前添加自定义目录地址（空格分隔）

### 3.4. 重新启动 jupyter notebook

重新启动 jupyter notebook，即可切换至自定义目录。

- 配置失败时，可以使用 `CMD/Powershell` 输入 `jupyter notebook` 查看启动时的报错，以对症下药。

## 4. 快捷键

- 命令模式按 `H` 或 `Help > Keyboard Shortcuts` 查看快捷键
- `Esc` 和 `Enter` 分别切换到命令模式与编辑模式
- 命令模式边框左侧为蓝线，编辑模式边框左侧为绿线

### 4.1. 命令模式

- `A/B` 分别在活跃单元格上/下方插入新的单元
- `Y/M/1/2` 分别将活跃单元格变成代码单元/Markdown单元/标题1/标题2
- `D`,`D` 删除活跃单元格
- `K/↑` 选择上方单元格；`J/↓` 选择下方单元格
- `X/C/V/Shift+V` 分别表示剪切，拷贝，粘贴到下方，粘贴到上方
- `Shift+Space/Space` 向上/下滚动

### 4.2. 编辑模式

- `Ctrl + Enter` 运行整个单元块
- `Alt + Enter` 运行整个单元块并新建单元格

## 5. 扩展

- 安装 Nbextensions

```shell
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install -usr
```

### 5.1. 扩展推荐

1. Code Prettify: 格式化代码
2. Scratchpad: 添加暂存单元，可以在不修改笔记本内容的同时调试代码
3. Table of Contents(2): 收集笔记本中的所有标题，并显示在浮动窗口中

## 6. 技巧

### 6.1. 查看功能列表

运行如下命令查看功能列表

```shell
%lsmagic
```

- `%` 逐行运行命令；`%%` 逐单元运行命令

### 6.2. 添加交互式仪表盘

> Building Interactive Dashboards with Jupyter : <https://blog.dominodatalab.com/interactive-dashboards-in-jupyter>

运行如下命令导入软件包

```shell
from ipywidgets import widgets
```

### 6.3. 向 jupyter notebook 中添加 kernel

1. `conda install ipykernel`
2. 将环境写入notebook的kernel中 `python -m ipykernel install --user --name 环境名称 --display-name 内核名字`

### 6.4. 查看 jupyter notebook 查看 kernel

`jupyter kernelspec list`

### 6.5. 删除 jupyter notebook 中的 kernel

`jupyter kernelspec remove kernelname`

## 7. 探索

1. A gallery of interesting Jupyter Notebooks · jupyter/jupyter Wiki : <https://github.com/jupyter/jupyter/wiki/A-gallery-of-interesting-Jupyter-Notebooks>
2. Jupyter Notebook Viewer : <https://nbviewer.jupyter.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb>

## 8. 魔法操作符

> Jupyter魔法操作符 | Notebook Share: <https://supergis.gitbooks.io/git_notebook/content/doc/jupyter_magics.html>

- `%lsmagic` 获取 Magic 操作符列表
- `%%!` 执行多行 shell

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->