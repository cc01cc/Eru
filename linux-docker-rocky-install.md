---
title: Rocky Linux 安装 Docker Engine
copyright: BY-NC-ND
date: 2023-03-02 22:19:55
tags:
    - Linux
    - Rocky Linux
    - Docker
---

## 1. 参考

Install Docker Engine on RHEL <https://docs.docker.com/engine/install/rhel/>

## 2. 清理旧版本

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine \
                  podman \
                  runc
```

## 3. 方法一：从仓库安装

### 3.1. 建立仓库

```shell
sudo yum update
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/rhel/docker-ce.repo
```

### 3.2. 安装 Docker Engine

以下方法二选一

#### 3.2.1. 安装最新版本的 Docker Engine

```shell
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### 3.2.2. 安装特定版本的 Docker Engine

1. 列举仓库中可用的版本

    ```shell
    yum list docker-ce --showduplicates | sort -r
    ```

   - 返回示例

    ```shell
    docker-ce.s390x                3:20.10.8-3.el8                 docker-ce-stable
    docker-ce.s390x                3:20.10.7-3.el8                 docker-ce-stable
    <...>
    ```

1. 从第二列中选择并安装特定的版本

    ```shell
    sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io docker-buildx-plugin docker-compose-plugin
    ```

## 4. 方法二：使用脚本安装

运行如下脚本自动安装 Docker Engine

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh --dry-run
```

## 5. 启动 Docker 服务

```shell
sudo systemctl start docker
```

## 6. 测试 Docker Engine

```shell
sudo docker run hello-world
```

若返回一段相关信息并退出，则 Docker Engine 安装正常

```shell
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->