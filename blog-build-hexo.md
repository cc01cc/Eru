---
title: Hexo 博客搭建
copyright: BY-NC-ND
date: 2023-03-01 23:30:33
tags:
    - blog-build
    - hexo
categories:
    - blog-build
---

## 参考

1. 安装 文档 | Hexo <https://hexo.io/zh-cn/docs/>
2. 部署 | Hexo <https://hexo.io/zh-cn/docs/one-command-deployment>

## 安装

1. 安装 Git 和 NodeJS
2. 安装 hexo `npm install -g hexo-cli`

## 部署

1. 克隆 `https://github.com/cc01cc/cc01cc.github.io.git`
2. 复制 node_modules 目录 【金山文档】 node_modules <https://kdocs.cn/l/caq8jnRXBkHP>
3. 使用 `git subtree add --prefix=source https://github.com/cc01cc/Eru.git main` 获取子仓库（博文内容）
   1. `git subtree pull --prefix=source https://github.com/cc01cc/Eru.git main` 更新子仓库
   2. `git subtree push --prefix=source https://github.com/cc01cc/Eru.git main` 推送到子仓库
   3. `commit` 和主仓库一起提交即可，在子仓库 `push` 的时候，git 会自动处理属于子仓库的 `commit`

> git subtree 参考 <https://training.github.com/downloads/submodule-vs-subtree-cheat-sheet/>

*最开始尝试的是，`git submodule` 但是 vercel 无法拉取到 `submodule` 内容，所以更换为 `subtree`。

## 主题

1. fluid-dev/hexo-theme-fluid <https://github.com/fluid-dev/hexo-theme-fluid>
2. Hexo Fluid 用户手册 <https://fluid-dev.github.io/hexo-fluid-docs/>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->