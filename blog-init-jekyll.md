---
title: blog-init-jekyll
date: 2022-05-31
tags:
    - init
    - jekyll
    - blog-build
# excerpt: 最初的开始-jekyll
categories:
    - blog-build
---


## Jekyll 目录结构

```txt
.
├── _config.yml (配置)
├── _drafts (草稿)
|   └── initial-jekyll.md
├── _includes (需重用的内容)
|   ├── footer.html
|   └── header.html
├── _layouts (布局)
|   ├── default.html
|   └── post.html
├── _posts (存放文章)
|   ├── 2022-05-30-initial.md
|   └── 2022-05-31-initial-jekyll.md
|
├── index.html
|
└── about.md
```

## 加载 liquid

如果需要让 jekyll 为页面加载 `liquid` 需要在头部使用

```txt
---
---
```

## 博文链接

> Tags Filters | Jekyll • Simple, blog-aware, static sites: <https://jekyllrb.com/docs/liquid/tags/#linking-to-posts>

博文使用 `post_url` 标签引用链接

```liquid
# 去除 \
\{\% post_url 2022-05-31-name-of-post \%\}
```

## 参考

> Setup | Jekyll • Simple, blog-aware, static sites <https://jekyllrb.com/docs/step-by-step/01-setup/>

<!--
Copyright © 2022-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc/cc01cc>
-->