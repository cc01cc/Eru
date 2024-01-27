---
title: 软链接和硬链接
copyright: BY-NC-ND
date: 2023-04-10 17:33:23
tags:
    - file system
---

## 1. 定义

- **软链接**：软链接（也称为符号链接）是一种特殊的文件，它存储了目标文件或目录的路径信息。软链接可以跨文件系统，也可以指向目录。
- **硬链接**：硬链接是同一个文件的多个名称，它们指向同一个 inode 节点。硬链接不能跨文件系统，也不能指向目录。

## 2. 创建方法

> Windows 中 链接名在前，目标文件在后
>
> Linux 中 连接名灾后，目标文件在前

### 2.1. Windows

> 环境：命令提示符 (cmd) 或 PowerShell
>
> mklink | Microsoft Learn: <https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/mklink>

```cmd
# 创建 软链接（符号链接）（可以指向目录或文件）
mklink /d file_path_to_soft_link target_file_or_dir_path
# 创建 硬链接（仅允许指向文件）
mklink /h file_path_to_hard_link target_file_path
```

查看文件的硬链接

> hardlink - How can I find hard links on Windows? - Super User: <https://superuser.com/questions/366739/how-can-i-find-hard-links-on-windows>
>
> fsutil hardlink | Microsoft Learn: <https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/fsutil-hardlink>

```cmd
fsutil hardlink list <filename>
```

### 2.2. Linux

> 环境：shell

```shell
# 创建 软链接（符号链接）（可以指向目录或文件）
ln -s /target/dir/or/file soft_link_name
# 创建 硬链接（仅允许指向文件）
ln /target/file hard_link_name
```

查看目录内的硬链接

> <https://superuser.com/a/366748/1486631>

```shell
# +1 表示硬链接数 大于 1
find path/to/dir -type f -links +1
```

查看目录内的软链接

```shell
find path/to/dir -type l
```

## 3. 区别

- 跨文件系统：软链接可以跨文件系统，而硬链接不可以。
- 指向目录：软链接可以指向目录，而硬链接不可以。
- 指向不存在的文件：软链接可以指向不存在的文件，而硬链接必须指向已存在的文件。

## 4. 优势

- 软链接：软链接可以跨文件系统，也可以指向目录。它更灵活，更容易管理。
- 硬链接：硬链接可以让您为同一个文件创建多个名称，而不需要占用额外的磁盘空间。它还可以保护文件免受意外删除（必须所有硬链接删除后原始文件才会删除）。

## 5. 补充说明

不能跨文件系统的含义是指硬链接只能在同一个文件系统中创建，不能在不同的文件系统中创建。(狭义上的同一文件系统，)

> 文件系统是用于存储和组织文件的一种数据结构，它定义了文件如何存储在磁盘上以及如何访问这些文件。常见的文件系统包括 NTFS、FAT32、ext4 等。

如果您有一个文件，它有两个硬链接，那么这两个硬链接必须位于同一个文件系统中。如果您将这两个硬链接复制到另一个文件系统中，那么它们将变成两个单独的文件，而不再是硬链接。

举个例子，假设您有一个名为 `file1` 的文件，它位于 `/home/user/documents` 目录中。您可以在该目录中为该文件创建一个硬链接，命名为 `file2`。此时，`file1` 和 `file2` 都指向同一个文件，它们共享相同的内容。

```txt
/home/user/documents
├── file1
└── file2 (hard link to file1)
```

但是，如果您将 `file2` 复制到另一个文件系统中（例如从本地磁盘复制到 U 盘），那么 `file2` 将变成一个单独的文件，而不再是 `file1` 的硬链接。

```txt
/home/user/documents
├── file1
└── file2 (hard link to file1)

/media/usb
└── file2 (copy of file1, not a hard link)
```

## 6. 扩展

1. 符号链接、硬链接及其在 Windows 上的应用举例 - 少数派: <https://sspai.com/post/66834>
2. 尝试过 `Link Shell Extension` 但是会和 PowerToy 冲突，所以放弃了

> 本文部分内容改编自与 Microsoft Bing 的对话。

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->