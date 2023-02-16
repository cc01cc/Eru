---
title: 最初的开始-jekyll
description: 这是一切开始的地方
date: 2022-05-31
slug: initial-blog-jekyll
categories:
    - 最初的开始
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

---

- 文章系个人学习总结，希望可以给大家带来些许启发，欢迎提出建议或给予指正。
- 本作品采用[知识共享署名-相同方式共享 4.0 国际许可协议](https://creativecommons.org/licenses/by-sa/4.0/legalcode.zh-Hans)进行许可。
- 欢迎大家转载分享，转载请标明源地址，谢谢
