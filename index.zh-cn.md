---
title: 关于
menu:
    main: 
        weight: -90
        params:
            icon: user
---

## 关于我

- 学生党，常用昵称为 `零一` `cc01cc`
- 爱好写代码，追番

## 技能

- Python 机器学习方向
- Java 后端方向
- HTML/CSS/JS 等基础前端
- 持续学习中（Rust, Java 进阶, Python 进阶等）

## 关于本站

- 这里是 cc01cc's blog, 由 cc01cc 建立于 2022 年 5 月 30 日
- 使用 `hugo` 作为框架，`hugo-theme-stack` 作为主题
- 部署：
  - `GitHub Pages`: <https://cc01cc.github.io/>
  - `Vercel`: <https://cc01cc.com/>

## url 规范

### 目标

易于辨识，不重复

### 要求

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

### 解决方案

单层级，全小写英文 `/blog/标签1-标签2-年月日`

1. 标签1 + 标签2
   1. 提高辨识度
   2. 大幅降低重复率
   3. 3 个标签过长
   4. 易于后期优化
2. 年月日
   1. 大幅降低重复了
   2. 易于后期归档

### 参考

1. http - 代码规范 - URL规范_个人文章 - SegmentFault 思否: <https://segmentfault.com/a/1190000019086744>

---

## 建站日志

### 2023年1月

#### 1月30日

- 开始将博客迁移到 Hexo

### 2022 年 11 月

#### 11 日

- 开始博客的搭建计划（Hugo）

#### 12 日

- 完成博客的本地搭建和运行

#### 13 日

- 改用 Hugo 完成博客的搭建和部署
- 完成博文的迁移工作
- 发布第一篇博文（Hugo）

### 2022年6月

#### 1 日

1. 新建 `default.html` 文件
2. 调整 `index.html` 首页，实现 `liquid` 语句渲染
3. 拆分 `about.html` 至 `about.md`, `log.md`

### 2022 年 5 月

#### 30日

1. 建立 cc01cc.github.io
2. 上传了第一篇博客（但发布乱码）

#### 31日

1. 参考 jekyll 教程，更新了仓库的结构
2. 成功加载第一篇博客