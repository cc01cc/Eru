---
title: MySQL (zip) 安装 (windows)
copyright: BY-NC-ND
date: 2023-06-09 22:30:34
tags:
    - from-mine
    - database
    - mysql
categories:
    - database
---

> MySQL :: MySQL 8.0 Reference Manual :: 2.3.4 Installing MySQL on Microsoft Windows Using a noinstall ZIP Archive: <https://dev.mysql.com/doc/refman/8.0/en/windows-install-archive.html>

## 1. 下载

MySQL Community Downloads: <https://dev.mysql.com/downloads/mysql/>

如下图，选上一个，不要选 `Debug Binaries & Test Suite`

![MySQL-Community-Downloads-20230610012222](https://v01.static.cc01cc.cn/MySQL-Community-Downloads-20230610012222.png)

## 2. 解压

解压 MySQL 文件到指定目录（常用/默认路径：`C:\mysql`）

## 3. 创建配置文件

> 配置文件读取列表 :: MySQL 8.0 Reference Manual :: 4.2.2.2 Using Option Files: <https://dev.mysql.com/doc/refman/8.0/en/option-files.html>

在 `%WINDIR%` 目录 (一般为 `C:/windows`) 下创建 `my.ini` 配置文件

*在命令行中使用 `echo %WINDIR%` 命令，可以查看 `%WINDIR%` 目录

### 3.1. 配置文件参考

```ini
[mysqld]
# set basedir to your installation path
basedir=E:\\mysql
# set datadir to the location of your data directory
datadir=E:\\mydata\\data
```

## 4. 初始化 data 目录

> MySQL :: MySQL 8.0 Reference Manual :: 2.10.1 Initializing the Data Directory: <https://dev.mysql.com/doc/refman/8.0/en/data-directory-initialization.html>

在 MySQL 的根目录运行以下命令，初始化 data 目录

```bash
# 随机生成密码
.\bin\mysqld --initialize --console
# 不使用密码
.\bin\mysqld --initialize-insecure --console
```

保存输出内容中的密码

```txt
[Note] [MY-010454] [Server] A temporary password is generated for root@localhost: Dr=LsUmeM3uC
```

## 5. 初次启动服务，验证配置

> MySQL :: MySQL 8.0 Reference Manual :: 2.3.4.5 Starting the Server for the First Time: <https://dev.mysql.com/doc/refman/8.0/en/windows-server-first-start.html>

在 MySQL 的根目录运行以下命令，启动服务

```bash
bin\mysqld --console
```

如果有如下类似输出，表明 MySQL 服务启动成功

```bash
mysqld: ready for connections
Version: '8.0.29'  socket: ''  port: 3306
```

## 6. 配置系统环境变量

将 MySQL 的 `\bin` 目录添加到系统环境变量 Path 中

这样就可以全局直接使用 MySQL 命令了。

## 7. 将 MySQL 添加到 Windows 服务中

> MySQL :: MySQL 8.0 Reference Manual :: 2.3.4.8 Starting MySQL as a Windows Service: <https://dev.mysql.com/doc/refman/8.0/en/windows-start-service.html>

使用 **管理员权限** 运行以下命令安装 MySQL 服务

*在实测时，发现需要使用绝对路径，具体原因还没整明白

```bash
# 自动安装（默认配置）
C:\zeoapp\mysql\bin\mysqld --install
# 手动安装
C:\zeoapp\mysql\bin\mysqld --install-manual
```

```bash
# 手动启动 mysql 服务
SC START mysql
```

使用默认配置安装后，MySQL 服务将随着系统自动启动

### 7.1. 移除 MySQL 服务

```bash
# 方法一
SC DELETE mysql
# 方法二
mysqld --remove
```

## 8. 修改 root 账户密码

运行以下命令

```bash
mysql -u root -p
```

输入之前保留的密码（在我的使用中，发现密码无法粘贴，并且会显示占位符`*`）

成功连接 mysql 后，使用以下命令，修改密码

```bash
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root-password';
```

## 9. 其他参考

mysql-8.0.16-winx64.zip安装教程详解 - 知乎: <https://zhuanlan.zhihu.com/p/48531203>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->