---
title: 零一的个性化-字体
copyright: BY-NC-ND
date: 2023-06-07 18:07:47
tags:
    - font
    - personalized
    - from-mine
categories:
    - persionalized
---

- [1. 字体选择标准](#1-字体选择标准)
- [2. 字体字重选择](#2-字体字重选择)
- [3. 字体的场景应用](#3-字体的场景应用)
  - [3.1. 中文文本](#31-中文文本)
  - [3.2. 代码编程](#32-代码编程)
  - [3.3. 中英文文本](#33-中英文文本)
  - [3.4. 远古命令行](#34-远古命令行)
- [4. 部分概念收集](#4-部分概念收集)
  - [4.1. 字体类型](#41-字体类型)
  - [4.2. OTF TTF .otf .ttf 区别](#42-otf-ttf-otf-ttf-区别)
    - [4.2.1. True Type Fonts (TTF)](#421-true-type-fonts-ttf)
    - [4.2.2. Open Type Fonts (OTF)](#422-open-type-fonts-otf)
  - [4.3. 点阵字体与矢量字体的区别](#43-点阵字体与矢量字体的区别)
  - [4.4. 微调 (hinting)](#44-微调-hinting)
- [5. 其他说明](#5-其他说明)
- [6. 开源许可证](#6-开源许可证)
  - [6.1. IPA Font License 1.0](#61-ipa-font-license-10)
  - [6.2. SIL Open Font License 1.1](#62-sil-open-font-license-11)
- [7. 感谢](#7-感谢)

> 本文具有极强的主观性，但也希望可以给大家提供些许帮助

## 1. 字体选择标准

1. 用于代码的字体：可以区分明确区分 `1lI` 和 `0Oo`
2. 具有明确的开源许可协议（一般为 SIL Open Font License 1.1 或 IPA Font License 1.0）
3. 听闻部分字体会对特定像素进行优化，挑选时可以关注一下
4. 字库相对成熟完整
5. 阅读体验舒适（主观感受）

| 字体           | 等宽 | 区分 `0Oo` | 区分 `1lI` | 许可证                    | 链接                                              |
| -------------- | ---- | ---------- | ---------- | ------------------------- | ------------------------------------------------- |
| Fira Code      | ✔    | ✔          | ✔          | SIL Open Font License 1.1 | <https://github.com/tonsky/FiraCode>              |
| JetBrains Mono | ✔    | ✔          | ✔          | SIL Open Font License 1.1 | <https://github.com/JetBrains/JetBrainsMono>      |
| cascadia code  | ✔    | ✔          | ✔          | SIL Open Font License 1.1 | <https://github.com/microsoft/cascadia-code>      |
| 霞鹜文楷       |      |            |            | SIL Open Font License 1.1 | <https://github.com/lxgw/LxgwWenKai>              |
| 更纱黑体       |      |            |            | SIL Open Font License 1.1 | <https://github.com/be5invis/Sarasa-Gothic>       |
| 思源宋体       |      |            |            | SIL Open Font License 1.1 | <https://github.com/adobe-fonts/source-han-serif> |
| 思源黑体       |      |            |            | SIL Open Font License 1.1 | <https://github.com/adobe-fonts/source-han-sans>  |

*霞鹜文楷字体集中含有等宽字体可以区分 `1lI` 和 `0Oo`。

## 2. 字体字重选择

- 代码：SemiBold > medium,
- 正文：regular/默认 > Light > medium
- 安装：regular, medium, SemiBold (若无，则Bold)

## 3. 字体的场景应用

- word 中一般需要调整 布局 > 文档网络；或固定行高。
- 偏好程度由高到低

### 3.1. 中文文本

- **霞鹜文楷（等宽）**: 引号为半角
- **思源黑体**
- **（等距）更纱黑体 SC** : 可以用在命令行内
- **思源宋体（SemiBold）** : 默认的思源宋体总觉的字重有些细

> 字体测试集选取主要是依据平常的经验，关于中文文本的选取参考了：[關於「南去經三國，東來過五湖」](https://blog.justfont.com/2014/12/jfbook-example/)

![中文字体对比图.png](https://raw.githubusercontent.com/cc01cc/zeorep/main/pic/202212291131486.png)

- Tips: 思源字体从 word 导出会转化为图片（放大会失真），之前就遇到了但一直不知道怎么解决，在这儿需要留意留意。

![思源字体导出变成图片](https://raw.githubusercontent.com/cc01cc/zeorep/main/pic/202212291131237.png)

### 3.2. 代码编程

- **Cascadia Code (/Mono) PL** : Mono 版本没有连字（推荐使用 ttf variable 安装版本）
  - 普通版本的 Cascadia Code/Mono 在 eclipse 存在乱码的情况
  ![Cascadia Code 乱码实录](零一的个性化-字体.zeobit/零一的个性化-字体.md_2022-02-24-19-29-13.png)
- **JetBrains Mono Medium**
- **Fira Code Medium**

关于代码的字体比较，网上也有许多参考，在这儿我就不献丑了。

在 Windows 环境下，可以配置多个字体参数时我常会使用：
`'Cascadia Mono', 'JetBrains Mono Medium', 'Fira Code Medium', 'Consolas', 'Courier New', '霞鹜文楷等宽', 'monospace'`

### 3.3. 中英文文本

> 可以直接使用 霞鹜文楷，思源黑体等，他们的英文字体也挺舒服的。但如果需要区分 `1lI0Oo` 可以下边的搭配或许提供些帮助，一般是是字重上的微调。

- 仅霞鹜文楷等宽
- 霞鹜文楷/思源宋体
  - 英文会选择字重细一些
  - **Cascadia Code Light**
  - **Fira Code (Light)**
  - **JetBrains Mono ExtraLight(/Light)**
- 思源黑体/更纱黑体（中文字重会选择细些）
  - 英文字重会选择粗些
  - **Cascadia Code**
  - **Fira Code**
  - **JetBrains Mono Medium**

### 3.4. 远古命令行

- **Cascadia Coda (/Mono)**
- **Sarasa Mono Slab CL**

## 4. 部分概念收集

> 这块内容查阅了大量相关资料，但由于涉及知识较为专业，如有表述错误，还望各位大佬赐教

### 4.1. 字体类型

> Serif, Sans, Script & Slab: 4 Font Types Explained :  <https://designshack.net/articles/typography/font-types-explained-serif-sans-script-slab/>

- monospace: 等宽（一般针对西文，中文字符本来就等宽）
- sans-serif: 无衬线
- serif: 有衬线
- slab: 一般较为厚重，适用于强调性文本，标题等，不适用于长文本
- VF (Variable fonts) : 可变字体，可以自由的调整字体的粗细

补充

- 不一定所有中文字体都是全角字符，如 霞鹜文楷的引号就是半角字符
- 等宽的字体，英文常为中文字符的一半宽度，视场景以及个人喜好自行选择

### 4.2. OTF TTF .otf .ttf 区别

OTF 相对于 TTF 是一个较新的数字字体标准，由 Adobe 和 Microsoft 共同开发。

1. `.otf` 是指基于 PostScript 开发的 OTF 格式 （windows 对其支持不佳，例如：word 无法将这类字体嵌入到 pdf 中）
2. `.ttf` 包含两类字体：
   1. 一类是古老的 TTF 格式；
   2. 另一类是 基于 TTF 开发的 OTF 格式

- `.ttc (TrueType Collection)` 是 `ttf (TrueType Collection)` 的集合。

   [ref] Differences and similarities between .ttf and .ttc fonts : <https://graphicdesign.stackexchange.com/questions/127828/differences-and-similarities-between-ttf-and-ttc-fonts>

> 以下内容翻译自：From OTF to TTF: How to Choose the
> Right Font? | Blog | 356labs : <https://356labs.com/blog/from-otf-to-ttf-how-to-choose-the-right-font/>

#### 4.2.1. True Type Fonts (TTF)

TrueType 是一个矢量字体的标准，由 Apple 和 Microsoft 在 1980 年代末开发，作为 Adobe 的 Type 1 的竞争对手。他们的目标是建立一个跨平台的字体格式。
TrueType 字形使用二次贝塞尔曲线，相比于三次曲线，它在数学上更加简单，处理上更加快速，但是需要更多的点去描述。这导致把 Type 1 字体自动转换为 TrueType 将会是一场灾难。而且，TrueType 字体的 hints 比 Type 1 更加完善和精确。
这意味着字体在任意大小都可以精确地显示，例如，你可以网页上放心地使用。
在很长的一段时间里，人们将 Post Script 字体用于打印，True Type 字体用于显示。

#### 4.2.2. Open Type Fonts (OTF)

OpenType 是数字字体的一个新的标准，由 Adobe 和 Microsoft 共同开发。这次他们制作字体格式的目标不仅是支持各类平台，而是支持世界范围的书写系统。
它建立在 TrueType 格式上，但也支持 PostScript 格式。就在这里出现了一个易于混淆的地方，基于 TrueType 的 OpenType 字体使用 `.ttf` 扩展名；而基于 PostScript 的 OpenType 字体使用 `.otf` 扩展名。
类似 TrueType，OpenType 也是一种跨平台的格式，但是更易于操作系统处理，这使得文件更轻便，处理更迅速。
OpenType 字体基于 Unicode 标准，因此它可以支持世界上任意一种语言。每个字体文件可以由多达 65536 个字符组成，切换语言可以变为非常简单的任务。
OpenType 另一个巨大优势是允许专业设计软件 (如 Adobe Illustrator, Photoshop, InDesign) 对它进行设计。例如：小型大写字母，替代字符或连字。这为设计师们提供了更多的灵活性，他们可以为您的材料提供更多的个性化。

### 4.3. 点阵字体与矢量字体的区别

> Linux字体美化实战 - 作者：金步国 : <http://www.jinbuguo.com/gui/linux_fontconfig.html>

- 点阵字体
  - 优点：低像素下保持清晰锐利的笔画
  - 缺点：不能缩放
- 矢量字体
  - 优点：可以任意缩放
  - 缺点：低像素下的表现并不突出

### 4.4. 微调 (hinting)

微调(hinting)分为两种：内嵌微调与自动微调。内嵌微调是字体设计者耗费大量的时间和精力、精心制作的、内嵌在字体文件中的额外指令，本质上是人工微调；而自动微调(autohint)是 FreeType 内嵌的一套微调算法，通用于所有矢量字体，本质上是机器微调。一般说来，内嵌微调比自动微调的显示效果更佳。

## 5. 其他说明

- 最近发现的一个网站：猫啃网：<https://www.maoken.com/> 整理了挺多字体的，感觉不错的样子。（我一般会从中参考一些开源的字体，商免的字体，怎么说呢，授权协议不太清晰，而且限制也各有不同）

> 一些字体有自己的命名规范一定要查看字体的官方说明

- sarasa 更纱黑体
  - 摘自 : <https://github.com/be5invis/Sarasa-Gothic#what-are-the-names>
  - Latin/Greek/Cyrillic character set being Inter
    - Quotes (`“”`) are full width —— **Gothic**
    - Quotes (`“”`) are narrow —— **UI**
  - Latin/Greek/Cyrillic character set being Iosevka
    - Em dashes (`——`) are full width —— **Mono**
    - Em dashes (`——`) are half width —— **Term**
    - No ligature, Em dashes (`——`) are half width —— **Fixed**
  - Orthography dimension
    - `CL`: Classical orthography
    - `SC`, `TC`, `J`, `K`, `HC`: Regional orthography, following [Source Han Sans](https://github.com/adobe-fonts/source-han-sans) notations.

## 6. 开源许可证

### 6.1. IPA Font License 1.0

- 许可证文本：<https://moji.or.jp/ipafont/license/>
  - （备用链接）<https://opensource.org/licenses/IPA>
- 许可证摘要：<https://www.tldrlegal.com/l/ipa>
  - 仅作参考，具体内容请参考许可证[原文](https://moji.or.jp/ipafont/license/)
  - 可商用，可修改，可重分发
  - 重分发不可使用字体名称，字体贡献者名称等信息进行推广
  - 贡献者不承担任何责任，使用者自行承担损失
  - 重分发需要包括原始字体与许可证

### 6.2. SIL Open Font License 1.1

- 许可证文本：<https://scripts.sil.org/OFL_web>
  - （备用链接）<https://opensource.org/licenses/OFL-1.1>
- 许可证摘要：<https://www.tldrlegal.com/l/ofl>
  - 仅作参考，具体内容请参考许可证[原文](https://scripts.sil.org/OFL_web)
  - 可商用，可修改，可重分发
  - 重分发不可更改许可证
  - 不可单独售卖字体
  - 贡献者不承担任何责任，使用者自行承担损失
  - 重分发需要此版权声明与许可证

## 7. 感谢

最后的最后，感谢 [lxgw](https://github.com/lxgw), [be5invis](https://github.com/be5invis) 等各位开源工作者以及开源社区为我们提供了如此优秀的字体。

<!--
Copyright © 2021-2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->