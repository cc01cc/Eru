---
title: Pandoc 使用指南
copyright: BY-NC-ND
date: 2023-05-30 22:55:54
tags:
    - software
    - from-mine
categories:
    - software
---

> 文档文件格式转换

## 快速开始

```shell
pandoc ./pandoc-lab/demo.ipynb -f ipynb -t markdown -o ./pandoc-lab/demo.md -t gfm
pandoc ./1.pdf -f pdf -t docx -o ./1.docx
```

- `./pandoc-lab/demo.ipynb` 原始文件路径
- `-f` 原文件格式
- `-t` 目标文件格式
- `-o` 目标文件路径
- `-t gfm` Github-Flavored Markdown 类型 markdown
  - markdown-variants - Pandoc User’s Guide: <https://pandoc.org/MANUAL.html#markdown-variants>

## 更多技巧

1. 进入用户手册: <https://pandoc.org/MANUAL.html>
   1. (PDF 版本): <https://pandoc.org/MANUAL.pdf>
   2. 在 zip 压缩包中有 html 版本的用户手册
2. 搜索原文件格式，查看相关配置以及注意事项
3. 搜索目标文件格式，查看相关配置以及注意事项

## 相关链接

1. Pandoc - About pandoc: <https://pandoc.org/index.html>
2. jgm/pandoc - GitHub: <https://github.com/jgm/pandoc>
3. **用户手册** Pandoc - Pandoc User’s Guide: <https://pandoc.org/MANUAL.html>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->