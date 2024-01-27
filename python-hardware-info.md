---
title: 使用 python 获取硬件信息
copyright: BY-NC-ND
date: 2023-03-16 20:28:39
tags:
    - python
    - gpu
    - cpu
    - memory
categories:
    - python
---

## 1. 获取内存信息

### 1.1. 使用 psutil 获取内存信息

> psutil 为 python 内置组件，不需要安装

可以应用于获取**实时**内存占用等场景

1. 引用 psutil

    ```python
    import psutil
    ```

2. 获取物理内存信息

    ```python
    virtual_memory_status = psutil.virtual_memory()
    # 转为字典格式
    virtual_memory_status = psutil.virtual_memory()._asdict()
    ```

3. 获取交换内存信息

    ```python
    swap_memory_status = psutil.virtual_memory()
    # 转为字典格式
    swap_memory_status = psutil.virtual_memory()._asdict()
    ```

## 2. 获取 CPU 信息

### 2.1. 使用 py-cpuinfo 获取 CPU 信息

1. 安装 py-cpuinfo

    ```shell
    pip install py-cpuinfo
    ```

2. 引用 py-cpuinfo

    ```python
    import cpuinfo
    ```

3. 获取 CPU 信息

    ```python
    cpu_info = cpuinfo.get_cpu_info()
    ```

### 2.2. 使用 psutil 获取 CPU 使用率

> psutil 为 python 内置组件，不需要安装

可以应用于获取**实时** CPU 使用率等场景

1. 引用 psutil

    ```python
    import psutil
    ```

2. 获取 CPU 使用率

    ```python
    cpu_percent = psutil.cpu_percent()
    ```

## 3. 获取 GPU 信息

### 3.1. 使用 gpustat 获取 GPU 信息

可以应用于**实时**获取 显存 占用等场景

1. 安装 gpustat

    ```shell
    pip install gpustat
    ```

2. 引用 gpustat

    ```python
    import gpustat
    ```

3. 获取 gpu 信息

    ```python
    gpu_info = gpustat.GPUStatCollection.new_query().jsonify()['gpus'][0]
    ```

输出参考

```txt
# 源于 Colab 的 GPU
{'index': 0, 'uuid': 'GPU-ce995437-a7da-2750-8e6b-3029bff55ef4', 'name': 'NVIDIA A100-SXM4-40GB', 'temperature.gpu': 32, 'fan.speed': None, 'utilization.gpu': 0, 'utilization.enc': 0, 'utilization.dec': 0, 'power.draw': 50, 'enforced.power.limit': 400, 'memory.used': 446, 'memory.total': 40960, 'processes': []}
```

### 3.2. 使用 numba 获取 NVIDIA GPU 名称

1. 安装 numba

    ```shell
    pip install numba
    ```

2. 从 numba 引用 cuda

    ```python
    from numba import cuda
    ```

3. 判断是否有 NVIDIA GPU

    ```python
    cuda.is_available()
    ```

4. 获取 NVIDIA GPU 名称

    ```python
    gpu_name = cuda.get_current_device()
    ```

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->