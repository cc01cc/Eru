---
title: guide-url
date: 2023-02-26 00:51:51
tags:
excerpt: url 规范
---

## 目标

易于辨识，不重复

## 要求

1. 采用小写英文
   1. 易于用户输入
   2. 部分服务器或 robots 区分大小写
2. 采用 `-` 作为连接符
   1. `-` 会被替换为空格
   2. `_` 会被省略
3. 目录或索引页以 `/` 结尾
   1. e.g. `cc01cc.com/blog/`
4. 层级采用降级结构，且不得超过三级
   1. e.g. `cc01cc.com/blog/2022/11/index.html`
5. 静态化页面禁止使用参数

## 解决方案

单层级，全小写英文 `/blog/标签1-标签2-年月日`

1. 标签1 + 标签2
   1. 提高辨识度
   2. 大幅降低重复率
   3. 3 个标签过长
   4. 易于后期优化
2. 年月日
   1. 大幅降低重复了
   2. 易于后期归档

## 参考

1. http - 代码规范 - URL规范_个人文章 - SegmentFault 思否: <https://segmentfault.com/a/1190000019086744>

<!--
Copyright © 2022-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc/cc01cc>
-->