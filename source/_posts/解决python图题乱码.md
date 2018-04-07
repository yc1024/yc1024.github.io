---
title: 解决python图题乱码
date: 2016-06-05 18:32:04
tags: python
---

### 在用python的时候经常会遇到乱码问题
#### 1. 注释乱码问题
在代码的最上面添加：
```python
# -*- coding: utf-8 -*-
```
#### 2. 无法识别中文字体
通过运行以下代码查看系统中可以用的中文字体：
```python
#! /usr/bin/env python
# -*- coding: utf-8 -*-
from matplotlib.font_manager import FontManager
import subprocess

fm = FontManager()
mat_fonts = set(f.name for f in fm.ttflist)

output = subprocess.check_output(
    'fc-list :lang=zh -f "%{family}\n"', shell=True)
# print '*' * 10, '系统可用的中文字体', '*' * 10
# print output
zh_fonts = set(f.split(',', 1)[0] for f in output.split('\n'))
available = mat_fonts & zh_fonts

print '*' * 10, '可用的字体', '*' * 10
for f in available:
    print f
```
<!-- more -->
加入以下语句：
```python
from pylab import *
mpl.rcParams['font.sans-serif'] = ['Droid Sans Fallback']
```
注：Droid Sans Fallback 为查询得到的系统中的中文字体
#### 3. 画图时候“-”号显示为方块问题
加入以下语句：
```python
mpl.rcParams['axes.unicode_minus'] = False
#解决保存图像是负号'-'显示为方块的问题
```
参考文献
[1] http://www.cnblogs.com/wei-li/archive/2012/05/23/2506940.html#oo
[2] http://old.sebug.net/paper/books/scipydoc/index.html#id2
