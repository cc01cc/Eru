---
title: Use Github
description: 使用 GitHub 的一些小技巧
date: 2022-06-06
slug: use-github
categories:
    - 最初的开始
---

## 高级搜索

1. 【高级搜索页】GitHub · Where software is built: <https://github.com/search/advanced>
2. 【帮助文档】About searching on GitHub - GitHub Docs: <https://docs.github.com/en/search-github/getting-started-with-searching-on-github/about-searching-on-github>

## 快捷键

> Keyboard shortcuts - GitHub Docs: <https://docs.github.com/en/get-started/using-github/keyboard-shortcuts>

*不区分大小写

1. `t` 激活文件查找器
2. `l` 跳转至代码的某一行

## 在线运行项目

1. Gitpod: Always ready to code.: <https://www.gitpod.io/>
2. 在 `url` 前添加 `https://gitpod.io#` 即可

## Codespaces

1. GitHub 代码空间文档 - GitHub Docs <https://docs.github.com/cn/codespaces>

### Java & Maven

```json
{
  "image": "mcr.microsoft.com/devcontainers/universal:2",
  "features": {
    "ghcr.io/devcontainers/features/java:1": {
        "version": "17",
        "jdkDistro": "ms",
        "installGradle": "false",
        "gradleVersion": "latest",
        "installMaven": "true",
        "mavenVersion": "latest" 
    }
  }
}
```

---

- 文章系个人学习总结，希望可以给大家带来些许启发，欢迎提出建议或给予指正。
- 本作品采用[知识共享署名-相同方式共享 4.0 国际许可协议](https://creativecommons.org/licenses/by-sa/4.0/legalcode.zh-Hans)进行许可。
- 欢迎大家转载分享，转载请标明源地址，谢谢
