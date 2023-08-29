---
title: Latex 指南
copyright: BY-NC-ND
date: 2023-05-28 22:18:13
tags:
    - software
    - latex
    - from-mine
categories:
    - software
---

## 1. 学习资料

1. 【视频教程】latex中文教程-15集从入门到精通包含各种latex操作- 哔哩哔哩 : <https://www.bilibili.com/video/av16002978>
2. Latex 符号集 - KaTeX : <https://katex.org/docs/supported.html>
3. tug.org/twg/mactex/tutorials/ltxprimer-1.0.pdf : <http://tug.org/twg/mactex/tutorials/ltxprimer-1.0.pdf>
4. dralpha.altervista.org/zh/tech/lnotes2.pdf : <http//dralpha.altervista.org/zh/tech/lnotes2.pdf>

## 2. Latex模板网站

1. LaTeX Templates - <http://www.latextemplates.com/>

## 3. 常用操作

```shell
# 调用帮助文档
texdoc
```

空一行表示分段

## 4. 文档结构

- 标题
- 前言/摘要
- 目录
- 正文
  - 篇、章、节、小节、小段
    - 文字、公式
    - 列表：编号的、不编号的、带小标题的
    - 定理、引理、命题、证明、结论
    - 诗歌、引文、程序代码、算法伪码
    - 制表
    - 画图
- 文献
- 索引、词汇表

## 5. 数学模式

- 行内(inline)公式：使用一对符号 `$ $` 来标示,如 `$a+b=c$`。
- 显示(display)公式:
  - 简单的不编号公式用命令 `\[` 和 `\]` 标示（不推荐使用双美元符号 `$$ $$`）
  - 基本的编号的公式用 `equation` 环境。
  - 更复杂的结构，使用 `amsmath` 宏包提供的专门的数学环境。（不要
使用 `eqnarray` 环境）

## 6. 图表

Create LaTeX tables online – TablesGenerator.com : <https://tablesgenerator.com/>

LaTeX Tables Editor : <https://www.latex-tables.com/>

Convert Table to LaTex Table - Table Convert Online : <https://tableconvert.com/?output=latex>

## 7. 参考和引用

JabRef - Free Reference Manager - Stay on top of your Literature : <https://www.jabref.org/>

```latex
\begin{center}
\begin{table}
  \begin{minipage}{0.45\textwidth}
  \centering
  \resizebox{o.45\textwidth}{!}{\begin{tabular}{|l|l|l|l|l|}
  \hline
  年龄      & 人数/人  & 总费用/元        & 男/人  & 女/人  \\  \hline
  小于39岁   & 320   & 8582579.60   & 44   & 276  \\ \hline
  39岁-57岁 & 4472  & 115155344.10 & 1504 & 2968 \\ \hline
  57岁至75岁 & 11016 & 334766623.87 & 7878 & 3138 \\ \hline
  大于75岁   & 1913  & 72521288.12  & 1529 & 384  \\ \hline
  \end{tabular}}
  \end{minipage}

  \begin{minipage}{0.45\textwidth}
  \centering
  \begin{tabular}{|l|l|l|l|l|}
  \hline
  年龄      & 严重  & 一般   & 无   & 未分区 \\ \hline
  小于39岁   & 8   & 275  & 13  & 24  \\ \hline
  39岁-57岁 & 79  & 3858 & 123 & 412 \\ \hline
  57岁至75岁 & 516 & 9175 & 545 & 780 \\ \hline
  大于75岁   & 106 & 1360 & 294 & 153 \\ \hline
  \end{tabular}
  \end{minipage}
    
  \begin{minipage}{0.45\textwidth}
  \centering
  \begin{tabular}{|l|l|l|l|l|}
  \hline
  年龄      & 小于2天 & 2天-8天 & 8天-29天 & 29天以上 \\ \hline
  小于39岁   & 150  & 60    & 47     & 63    \\ \hline
  39岁-57岁 & 1847 & 985   & 815    & 825   \\ \hline
  57岁至75岁 & 2327 & 3381  & 2485   & 2823  \\ \hline
  大于75岁   & 286  & 418   & 525    & 684   \\ \hline
  \end{tabular}
  \end{minipage}

  \begin{minipage}{0.45\textwidth}
  \centering
  \begin{tabular}{|l|l|l|l|l|}
  \hline
  年龄      & 外科   & 非手术操作 & 内科   & 29天以上 \\ \hline
  小于39岁   & 197  & 0     & 123  & 63    \\ \hline
  39岁-57岁 & 2392 & 0     & 2080 & 825   \\ \hline
  57岁至75岁 & 5849 & 1     & 5166 & 2823  \\ \hline
  大于75岁   & 879  & 1     & 1033 & 684   \\ \hline
  \end{tabular}
  \end{minipage}
  \caption{疾病类型，年龄段，诊疗费用数据预处理}\label{问题三数据预处理}
\end{table}
\end{center}
```

## 8. 技巧

### 8.1. 实现Latex中文输入

> How does one type Chinese in LaTeX?<https://tex.stackexchange.com/questions/17611/how-does-one-type-chinese-in-latex>

```latex
% UTF-8 encoding
% Compile with latex+dvipdfmx, pdflatex, xelatex or lualatex
% XeLaTeX is recommended
\documentclass[UTF8]{ctexart}
\begin{document}
中文字符
\end{document}
```

or

```latex
\documentclass{article}
\usepackage[UTF8]{ctex}
```

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->