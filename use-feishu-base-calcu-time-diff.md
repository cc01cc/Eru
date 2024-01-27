---
title: 飞书-多维表格-计算时间差
copyright: BY-NC-ND
date: 2023-10-21 00:47:56
updated: 2023-10-21 00:01:17
tags:
---

## 1. 选择字段类型

1. 如图所示，字段类型选择 `公式`

    ![20231021010528](https://v01.static.cc01cc.cn/20231021010528.png)

## 2. 编辑公式

1. 单击 `公式编辑器`
2. 在弹出的公式编辑框中输入公式 `TEXT([终结时间]-[开始时间],"HH:MM")`
   1. `[终结时间]` 和 `[开始时间]` 请替换成你的表格中对应的字段名称
   2. `HH:MM` 表示输出的时间格式为 `时:分`
   3. 其中 "YYY/MM/DD HH:MM" 表示 年月日时分，可以自行选取合适的值

    ![20231021010919](https://v01.static.cc01cc.cn/20231021010919.png)

<!--
Copyright © 2023 [github.com/cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->