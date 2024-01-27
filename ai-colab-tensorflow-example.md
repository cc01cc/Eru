---
title: colab 中 安装 tensorflow example 报错以及解决方案
copyright: BY-NC-ND
date: 2023-04-23 10:47:31
tags:
    - ai
    - colab
    - tensorflow
categories:
    - ai
---


## 运行

```bash
!pip install git+https://github.com/tensorflow/examples.git
```

## 报错

```txt
Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
Collecting git+https://github.com/tensorflow/examples.git
  Cloning https://github.com/tensorflow/examples.git to /tmp/pip-req-build-u7_jdkn8
  Running command git clone --filter=blob:none --quiet https://github.com/tensorflow/examples.git /tmp/pip-req-build-u7_jdkn8
  Resolved https://github.com/tensorflow/examples.git to commit e3849ccb6d981aad311f0174281c8575d5e21646
  error: subprocess-exited-with-error
  
  × python setup.py egg_info did not run successfully.
  │ exit code: 1
  ╰─> See above for output.
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  Preparing metadata (setup.py) ... error
error: metadata-generation-failed

× Encountered error while generating package metadata.
╰─> See above for output.

note: This is an issue with the package mentioned above, not pip.
hint: See above for details.
```

![ai-colab-tensorflow-example-01](https://v01.static.cc01cc.cn/ai-colab-tensorflow-example-20230423141824.png)

## 解决方案

```bash
# 参考 https://github.com/tensorflow/tensorflow/issues/60106#issuecomment-1487638835
!apt remove git -y # remove any degraded git module
!apt-get install git -y && git clone https://github.com/tensorflow/examples.git # Install git first, then clone.
```

```python
# 参考 https://github.com/tensorflow/tensorflow/issues/60106#issuecomment-1511149579
import sys
sys.path.append('/content/examples') 
import tensorflow_examples
```

## 扩展

1. tensorflow/examples: TensorFlow examples: <https://github.com/tensorflow/examples>

## 同步

1. StackOverflow: How to install tensorflow examples in colab
   1. Q: <https://stackoverflow.com/q/76083008/15599248>
   2. A: <https://stackoverflow.com/a/76083019/15599248>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->