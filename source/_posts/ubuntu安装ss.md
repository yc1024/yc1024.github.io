---
title: ubuntu安装ss
date: 2018-04-30 07:01:24
tags:
---
最近需要科学上网,结果发现在ubuntu18上没有ss的源..那就源码编译搞起吧
### 安装`libqtshadowsocks-dev`
安装依赖
```
sudo apt-get install qt5-qmake qtbase5-dev libbotan1.10-dev pkg-config debhelper
```

安装`libqtshadowsocks-dev`

```
cd Downloads/
git clone --branch v1.10.0 https://github.com/shadowsocks/libQtShadowsocks.git
cd libQtShadowsocks/
dpkg-buildpackage -uc -us -b
sudo dpkg -i ../libqtshadowsocks_1.10.0-1_amd64.deb ../libqtshadowsocks-dev_1.10.0-1_amd64.deb
cd ..
```
### 安装`shadowsocks-qt5`
安装依赖
```
sudo apt-get install libqrencode-dev libzbar-dev libappindicator-dev
```
安装`shadowsocks-qt5`
```
git clone --branch v2.8.0 https://github.com/shadowsocks/shadowsocks-qt5.git
cd shadowsocks-qt5/
dpkg-buildpackage -uc -us -b
sudo dpkg -i ../shadowsocks-qt5_2.8.0-1_amd64.deb
```

启动ss
```
ss-qt5
```

Enjoy it ~

#### 参考文献
```
https://blog.whsir.com/post-883.html
```
