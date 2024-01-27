---
title: Python 日志模块使用
copyright: BY-NC-ND
date: 2023-04-30 11:03:24
tags:
    - python
    - log
categories:
    - python
---

## 将日志导出到文件【方法一】

```python
import logging

# https://docs.python.org/zh-cn/3/library/logging.html#logging.basicConfig
logging.basicConfig(
    filename='path/to/example.log', 
    format='%(asctime)s-%(name)s-%(levelname)s-%(message)s',
    level=logging.DEBUG
    )

logging.debug('Debug message')
logging.info('Info message')
logging.warning('Warning message')
```

*实测，Colab 中新建的日志文件只有当 running time 结束后才会出现。

## 将日志导出到文件【方法二】

```python
import logging

logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

formatter = logging.Formatter('%(asctime)s-%(name)s-%(levelname)s-%(message)s')

file_handler = logging.FileHandler('path/to/example.log')
file_handler.setFormatter(formatter)

logger.addHandler(file_handler)

logger.info('This is an Info message')
```

*实测，Colab 中此方法无法写入到文件，会输出到控制台，暂未找到原因。

## 参考/扩展

- logging - Python doc: <https://docs.python.org/zh-cn/3/library/logging.html>
- Logging in Python - Real Python: <https://realpython.com/python-logging/>
- logging_in_python.ipynb - Colaboratory: <https://colab.research.google.com/github/aviadr1/learn-advanced-python/blob/master/content/15_logging/logging_in_python.ipynb#scrollTo=WX5tMBMB28az>

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->