---
title: com 和 cn 站自动化部署时备案信息的处理
copyright: BY-NC-ND
date: 2023-04-07 21:50:27
tags:
    - blog-build
categories:
    - blog-build
---

## 原因

我的博客主要有两个站：境内的 cc01cc.cn 和 境外的 cc01cc.com

![cn-com-结构图](https://v01.static.cc01cc.cn/cn-com-01.jpg)

com 站，使用的是 GitHub 和 Vercel 的自动化部署服务，而且不需要付费；所以作为一个相对稳定的支撑。

cn 站，在境内我没有找到免费的服务，所以从定制化以及经济成本的角度，使用 DCDN + ECS + OSS 方案。

cn 站 和 com 站几乎全部的内容都一致，但是 cc01cc.cn 域名进行了 ICP 备案，根据 ICP 备案的要求【[浙江备案规则](https://help.aliyun.com/document_detail/50264.html#section-z5r-zxv-7ro)】：

1. 在主页底部的中央位置标明其备案编号
2. 要求链接信息产业部备案管理系统网址

但是 com 域名没有进行备案(境外服务器不支持备案)，所以这造成了两个站点需要同步，但又不完全同步

## 一代解决方案

第一代，我的思路是同一个 git 仓库，搭建两个分支，其中 cn 分支添加 备案信息，cn 站自动化部署的时候，使用 cn 分支的信息。

![cn-com-01-branch](https://v01.static.cc01cc.cn/cn-com-01-branch.jpg)

cn 分支添加备案信息之后，每次从 com 分支合并到 cn 分支，这样就不会影响到 com 分支，同时 cn 分支有 com 分支所没有的备案信息：

```bash
git checkout cn
git mrege com
git checkout com
```

同时添加阿里云云效仓库的 git地址 为 名为 `ali` 的远程地址，每次更新博客的时候分别将两个分支推送到两个远程仓库，分别触发各自的自动化部署程序

```bash
git push origin com
git push ali cn
```

但是存在一个问题：

1. 分支切换合并非常的繁琐，且一旦出错复原也相对繁琐

所以我考虑本地使用 com 仓库，阿里云 云效自动部署的时候，自动合并 com 到 cn 分支

但是发现

1. 阿里云云效-流水线拉取代码只拉取单条分支，checkout 的时候会新建分支，所以 merge 并没有用处

    ![仅拉取单条分支](https://v01.static.cc01cc.cn/20230407225029.png)

2. 如果直接在 cn 分支运行，云效-流水线拉取的是 origin 源，也就是 GitHub 的仓库，之后不知道为什么 cn 分支被 main 分支覆盖了

    ![拉取自 origin](https://v01.static.cc01cc.cn/20230407225537.png)

其他也进行了多次尝试，但是总是会遇到各种奇怪的问题，要么 main 分支被复写，要么 cn 分支被复写，也有 remote 信息被修改，综上我开始尝试其他的自动化部署方案

## 二代解决方案（当前使用）

一代尝试分支的方式不成功，之后我就在考虑只使用 main 分支，阿里云云效自动部署的时候，直接把备案信息写进去，其实改写的内容很简单，只需要把 `_config.fluid.conf` 配置文件中

```conf
  beian:
    enable: false
```

修改为 true 即可，由于 `enable: false` 这种语句太多，所以我在后边添加了个注释：

```conf
  beian:
    enable: false # beian
```

这样运行如下命令，即可自动修改为 ture

```bash
sed -i 's/enable: false # beian/enable: true # beian/' '_config.fluid.yml'
```

### 小提示

建议在最后构造的时候，修改配置文件，因为云效-流水线的构造代码来源是重新从仓库克隆的，所以在前边步骤修改了不提交到仓库也无用处

![克隆自仓库](https://v01.static.cc01cc.cn/20230407230735.png)

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->