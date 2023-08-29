---
title: 使用 PIL, OpenCV, Matplotlib 获取图片通道数
copyright: BY-NC-ND
date: 2023-05-24 12:05:49
tags:
    - ai
    - picture-processing
    - from-mine
categories: 
    - ai
---

## 1. PIL

```python
img = Image.open(img_path)
# getbands() 返回包含此图像中每个波段名称的元组。例如，RGB 图像返回 (“R”, “G”, “B”) 。
len(img.getbands())
```

> [参考] <https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.getbands>
>
> [参考] python - Number of channels in pil (pillow) image - Stack Overflow: <https://stackoverflow.com/questions/52962969/number-of-channels-in-pil-pillow-image>

## 2. OpenCV

```python
import cv2
img = cv2.imread(img_path, cv2.IMREAD_UNCHANGED)
# img.shape 包含三个值依次为垂直尺寸(高)，水平尺寸(宽)和通道数
img.shape[2]
```

## 3. ~~Matplotlib (plt)~~

> This function exists for historical reasons. It is recommended to use `PIL.Image.open` instead for loading images.

官方推荐使用 `PIL.Image.open` 读取图片，故这儿也不再展示 Matplotlib 读取图片的方式

> [参考] matplotlib.pyplot.imread — Matplotlib 3.5.2 documentation: <https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.imread.html>

## 4. 特殊情况(OpenCV, PIL 读取通道数结果不同)

### 4.1. 场景

在  **palette** 类型的图像中 (`img.mode`为**p**) ，也就是索引值组成的图像时，OpenCV 和 PIL 读取的通道数结果不同。

### 4.2. 原因

OpenCV 会自动加载扩展，将此类型图片转化为 RGB 图像处理，所以通道数会显示为 3；PIL 保留原始读取结果，所以通道数为 1。

综上在识别图片通道数时，个人更加推荐 **PIL** 。

> [参考] opencv - why does reading image with cv2 has different behavior from PIL? - Stack Overflow: <https://stackoverflow.com/questions/61952256/why-does-reading-image-with-cv2-has-different-behavior-from-pil>
>
> [扩展] python - What is the difference between images in 'P' and 'L' mode in PIL? - Stack Overflow: <https://stackoverflow.com/questions/52307290/what-is-the-difference-between-images-in-p-and-l-mode-in-pil/52307690#52307690>

<!--
Copyright © 2023 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->