---
title: 将 Hexo 博客部署到阿里云服务器（自动部署）
copyright: BY-NC-ND
date: 2023-03-16 22:57:26
tags:
    - blog-build
    - cloud server
    - aliyun
    - nginx
    - hexo
categories:
    - blog-build
---

## 1. 使用 阿里云 云效 自动部署

- 因为我的服务器是阿里云的 ecs 所以使用的是阿里云的 DevOps 服务
- 总体思路：创建自动构建流水线
- 这是我第一次使用 云效 如有更佳的方法欢迎探讨

### 1.1. 代码源

1. 【初始化】使用 token 从 Github 同步到 云效 代码仓库
2. 云效中添加 git ssh 公钥
3. 本地新增 云效代码仓库 远程地址
4. 添加 Webhook 当 指定的云效内的代码仓库变更时 自动触发流程

之后更新代码的时候，分别 push 到 GitHub 和 云效 即可。

- 因为 云效 直接获取 GitHub 仓库，需要授予 OAuth 权限，并且获取的权限相当多，所以没有授予。

### 1.2. 构建

1. **添加步骤** Node.js 构建
2. 选择 Node.js 版本
3. 添加 构建语句

    ```shell
    # cnpm 使用的是淘宝镜像源
    # 使用 npm 总是报 404，但 cnpm 能用，那就不执著于 npm 了 
    cnpm install
    cnpm run build
    ```

4. **添加步骤** 构建物上传
5. 选择上传方式以及制品名称（我在这儿全部保持默认）

### 1.3. 部署

1. 选择主机部署模板
2. 勾选部署时下载制品
3. 填写「构建」时制品的名称
4. 新建主机组（根据提示创建即可）
5. 配置下载路径（这是我的路径，仅供参考 `/home/hexo/package.tgz`）
6. 执行用户，我使用的是默认的 `root`
7. 部署脚本，如下（仅供参考）

    ```bash
    mkdir -p /home/hexo/tmp/
    tar zxvf /home/hexo/package.tgz -C /home/hexo/tmp/
    rm -rf /home/hexo/blog_zeo/*
    mv /home/hexo/tmp/public/* /home/hexo/blog_zeo/
    rm -rf /home/hexo/tmp/
    ```

8. 其余选项保持默认

## 2. 配置域名解析

- 因为域名解析配置完成，距离生效需要一定的时间，所以提到前边来
- 具体可以参考域名服务商的开发文档，以下提供基础思路

1. 添加 A 记录，值填写 IPv4 地址（创建了两条 A 记录，主机名分别为`空`和`www`）
2. 添加 AAAA 记录，值填写 IPv6 地址（创建了两条记录，主机名分别为`空`和`www`）

## 3. 配置 nginx

1. 下载并安装 nginx

    ```shell
    sudo dnf install nginx
    ```

2. 查看 nginx 位置信息

    ```shell
    whereis nginx
    ```

3. 配置 nginx

    > 此处不需要配置 443 端口，后边会自动化配置

    ```shell
    # 具体路径参考上一步骤
    sudo vim /etc/nginx/nginx.conf
    ```

    配置文件参考

    ```conf
    # 修改为刚刚创建的 hexo 用户
    user hexo;

    # ... 省略

    server {
        listen       80;
        listen       [::]:80;
        server_name  cc01cc.cn; # 此处修改为自己的域名

        # 此处修改为自己存放博客的地址
        root /home/hexo/blog_zeo;
        location / {
                index index.html index.htm;
        }
        # ... 省略
    }
    ```

4. 配置 `/home/hexo/blog_zeo` 权限为所有用户可读取

    ```bash
    sudo chmod -R a+r /home/hexo/blog_zeo
    ```

5. 重新加载 nginx

    ```shell
    nginx -s reload
    ```

6. 测试配置是否正确

    ```shell
    wget http://127.0.0.1
    ```

## 4. 开放防火墙端口

1. 添加端口规则

    ```shell
    sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
    sudo firewall-cmd --zone=public --add-port=443/tcp --permanent
    ```

2. 重新加载防火墙

    ```shell
    sudo firewall-cmd --reload
    ```

3. 查看 firewall 状态

    ```shell
    systemctl status firewalld
    ```

4. 查看端口开放状态（以 443/tcp 为例）

    ```shell
    firewall-cmd --zone=public --query-port=443/tcp
    ```

## 5. 开放服务器安全组端口

不同的服务器厂商的操作不一致，以下为大致思路

入站规则添加端口 `80`, `443` 允许的 ip 设置为 `0.0.0.0`, `::0`

## 6. 测试 http 访问

使用 http 通过域名访问，如果可以加载主页，说明配置成功，否则根据实际情况排查问题。

- 仅加载主页(index.html)即可，部分关联资源，可能使用了 https 所以无法加载

## 7. 开启 ssl 加密（https）

总体思路使用 certbot(nginx)

> 本样例使用并推荐 pip 方式，其他方式大多通过 snap，但是 snap 没有镜像站，境内下载较慢

1. 安装 Python 等依赖

    ```bash
    sudo dnf install python3 augeas-libs
    ```

2. 清理旧环境

    ```bash
    sudo dnf remove certbot
    sudo yum remove certbot
    sudo apt-get remove certbot
    ```

3. 配置 python 虚拟环境

    > 之后配置失败的话，直接把环境（目录）删除后重复操作即可

    ```bash
    sudo python3 -m venv /opt/certbot/
    sudo /opt/certbot/bin/pip install --upgrade pip
    ```

4. 安装 Certbot

    ```bash
    sudo /opt/certbot/bin/pip install certbot certbot-nginx
    ```

5. 添加 Cerbot 链接

    > 配置链接后，就可以直接使用 `cerbot` 命令了

6. 运行 Certbot 自动化配置

    ```bash
    # 根据提示操作即可
    sudo certbot --nginx
    ```

    当运行失败的时候，尝试检查（供参考）：

    - nginx.conf 的 server.name 是否和 域名一致
    - 域名解析地址是否正确（可以使用 ping 检查一下域名解析）

7. 配置自动更新

    ```bash
    echo "0 0,12 * * * root /opt/certbot/bin/python -c 'import random; import time; time.sleep(random.random() * 3600)' && sudo certbot renew -q" | sudo tee -a /etc/crontab > /dev/null
    ```

8. 验证配置

    使用 https 通过域名访问，如果访问成功则配置无误

9. 【每月】更新 cerbot

    ```bash
    sudo /opt/certbot/bin/pip install --upgrade certbot certbot-nginx
    ```

> Certbot Instructions | Certbot: <https://certbot.eff.org/instructions?ws=nginx&os=centosrhel8>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->