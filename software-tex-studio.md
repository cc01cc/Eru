---
title: TexStudio 指南
copyright: BY-NC-ND
date: 2023-05-28 22:24:03
tags:
    - software
    - from-mine
categories:
    - software
---

# software-tex-studio

## 1. 安装并配置 Tex Studio

1. 运行 texstudio 安装程序
   1. Latex Studio(可能被屏蔽) <https://www.texstudio.org/>
   2. Latex Studio(应该是个镜像，目前可以访问) <https://texstudio.sourceforge.net/>
2. 在 Tex Studio 的设置>构建选项卡中，调整默认编译器为 XeLaTeX（XeLaTeX 采用 UTF-8 编码支持中日韩文字）
3. 修改渲染方式（避免中文字符光标错位 bug）
	1. 参考 TeXstudio 中文光标定位不准确，如何解决？- 邓博元的回答 - 知乎
<https://www.zhihu.com/question/27604588/answer/37378185>
	2. 设置 > 显示高级选项 > 在左侧选择「高级编辑器」
	3. 取消勾选「自动选择最佳显示选项」（在底下）
	4. 勾选「关闭固定位置模式」（渲染模式保持默认的 QCE 即可）
	5. 保存设置

## 2. 常用快捷键

|快捷键|说明|
|--|--|
|F5|构建并查看|
|Ctrl+K|删除行|
|Alt+K|删除至行末|

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->
