---
title: 一款非常好用的流程图绘制工具graphviz
date: 2018-04-07 10:29:42
tags: 绘图工具
---
### graphviz 简介
本文介绍一个高效而简洁的绘图工具graphviz。graphviz是贝尔实验室开发的一个开源的工具包，它使用一个特定的DSL(领域特定语言): dot作为脚本语言，然后使用布局引擎来解析此脚本，并完成自动布局。graphviz提供丰富的导出格式，如常用的图片格式，SVG，PDF格式等。

### 基础知识
graphviz包含3中元素，图，顶点和边。每个元素都可以具有各自的属性，用来定义字体，样式，颜色，形状等。下面是一些简单的示例，可以帮助我们快速的了解graphviz的基本用法。

### graphviz的安装及使用(以centos为例)
```
yum install graphviz -y
dot -Tpng -odemo.png demo.gv // 假设代码在demo.gv文件中，执行该命令，生成demo.png的图片

```
### demo
比如，要绘制一个有向图，包含4个节点a,b,c,d。其中a指向b，b和c指向d。可以定义下列脚本：

```
digraph abc{
  a;
  b;
  c;
  d;
 
  a -> b;
  b -> d;
  c -> d;
}
```
![demo图](/img/graphvizdemo.png)

这里就只抛砖引玉，其余的图形这里就不再赘述了，需要的时候自行探索
BTW 推荐一款非常好用的在线url图绘制工具
```
https://www.processon.com/diagrams
```
### 参考文献
[1] http://icodeit.org/2015/11/using-graphviz-drawing/
