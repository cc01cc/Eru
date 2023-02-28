---
title: blog-init-jekyll
date: 2022-05-31
tags:
excerpt: 最初的开始-jekyll
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
