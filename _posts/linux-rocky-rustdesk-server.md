---
title: 安装 RustDesk 服务器 (适用 Rocky Linux, CentOS, RHEL 系列发行版)
copyright: BY-NC-ND
date: 2023-03-02 22:44:41
tags:
    - Linux
    - Rocky Linux
    - RustDesk
    - Docker
---

> 环境：Rocky Linux 9.1

## 1. 安装 Docker Engine

- 可以参考 [[linux-docker-rocky-install]] <https://cc01cc.com/2023/03/02/2023/03/02/linux-docker-rocky-install/>
- 英文可以参考官方文档 `Install Docker Engine on RHEL` <https://docs.docker.com/engine/install/rhel/>

## 2. 安装 Docker Compose

> <https://docs.docker.com/compose/install/linux/#install-using-the-repository>

```shell
sudo dnf update
sudo dnf install docker-compose-plugin
```

## 3. 验证 Docker Compose

```shell
docker compose version
```

## 4. 创建 Docker Compose 配置文件

> <https://rustdesk.com/docs/en/self-host/install/#docker-compose-examples>

1. 创建安装/运行目录并进入

    ```shell
    mkdir ~/zeodocker/rustdesk
    cd ~/zeodocker
    ```

2. 创建 Docker Compose 配置文件

    ```shell
    vi rustdesk-docker-compose.yml
    ```

    配置文件内容参考（记得修改服务器地址）：

    ```yml
    version: '3'

    networks:
    rustdesk-net:
        external: false

    services:
    hbbs:
        container_name: hbbs
        ports:
        - 21115:21115
        - 21116:21116
        - 21116:21116/udp
        - 21118:21118
        image: rustdesk/rustdesk-server:latest
        command: hbbs -r example.com:21117  // 更改为当前服务器的公网地址
        volumes:
        - ./data:/root
        networks:
        - rustdesk-net
        depends_on:
        - hbbr
        restart: unless-stopped

    hbbr:
        container_name: hbbr
        ports:
        - 21117:21117
        - 21119:21119
        image: rustdesk/rustdesk-server:latest
        command: hbbr
        volumes:
        - ./data:/root
        networks:
        - rustdesk-net
        restart: unless-stopped
    ```

## 5. 开放 端口

需要开放如下端口

```txt
TCP (21115, 21116, 21117, 21118, 21119)
UDP (21116)
```

### 5.1. 开放防火墙端口

1. 添加端口规则

    ```shell
    sudo firewall-cmd --zone=public --add-port=21115-21119/tcp --permanent
    sudo firewall-cmd --zone=public --add-port=21116/udp --permanent
    ```

2. 重新加载防火墙

    ```shell
    sudo firewall-cmd --reload
    ```

3. 查看 firewall 状态

    ```shell
    systemctl status firewalld
    ```

4. 查看端口开放状态（以 21116 udp 为例）

    ```shell
    firewall-cmd --zone=public --query-port=21116/udp
    ```

### 5.2. 开放云服务安全组入站端口

具体操作请参考各大云服务器厂商的相关文档。

配置入站时，授权对象含义参考：

- `0.0.0.0/0` ipv4 所有地址
- `::/0`ipv6 所有地址

## 6. 启动/重启 Docker

```shell
# 启动 Docker
sudo systemctl start docker
# 重启 Docker
sudo systemctl restart docker
# 查看 docker 服务状态
sudo systemctl status docker
```

## 7. 执行 rustdesk-docker-compose.yml

<https://docs.docker.com/compose/gettingstarted/>

```
docker compose up
```

## 8. 测试 RustDesk 服务器

配置 `远程客户端` 和 `本地客户端` 的 `ID 服务器` ，填入 RustDesk 服务器的公网地址

## 9. 强制 RustDesk 服务器连接加密

<https://rustdesk.com/docs/en/self-host/install/#key>

RustDesk 服务器启动时，会自动产生一对加密私钥和公钥

1. 配置强制连接加密，修改配置文件的 `16`, `31` 行，`hbbs`, `hbbr` 的运行命令添加 `-k _`参数

    ```shell
    command: hbbs -r example.com:21117 -k _// 改为当前服务器的公网地址
    command: hbbr -k_
    ```

2. 查看并复制公钥 （一般位于 `运行目录/data/`）

    ```shell
    cat ./id_ed25519.pub
    ```

3. 将公钥填入 `远程客户端` 和 `本地客户端` 的 `key` 中

## 10. 后台运行 RustDesk 服务器

```shell
docker compose up -d
```

## 11. 停止 RustDesk 服务

进入运行目录，后执行如下命令

```shell
docker compose stop
```

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->