---
title: "使用barrier在多台设备间共享鼠标和键盘"
date: 2023-08-01T15:22:27+08:00
draft: false
---

## 介绍

Barrier是一款开源的多平台的鼠标键盘共享软件，可以在多台设备间共享鼠标和键盘，支持Windows、Linux、MacOS等多种操作系统(不同平台(例如一台Windows,一台Linux)的设备也可以共享一套鼠标键盘)。

## 安装

### Windows

Winodws下安装很简单，直接下载这个[安装包](https://github.com/debauchee/barrier/releases)安装即可。

### Linux

各大发行版一般都有对应的包，例如Ubuntu可以直接使用`apt`安装：

```bash
sudo apt install barrier
```

### 使用说明

这个软件有两种模式，一种是服务端模式，一种是客户端模式。使用的时候需要一台充当服务端，其他的设备充当客户端, 启动服务端之后, 客户端只需要脸上服务端的IP地址即可, 非常简单。

使用过程中需要注意的点：

1. 最好去掉SSL选项

2. asfdasdfasdf

3. 