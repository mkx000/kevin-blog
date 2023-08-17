---
title: "使用barrier在多台设备间共享鼠标和键盘"
date: 2023-08-01T15:22:27+08:00
draft: false
---

## 介绍

Barrier是一款开源的多平台的鼠标键盘共享软件，可以在多台设备间共享鼠标和键盘，支持Windows、Linux、MacOS等多种操作系统，不同平台(例如一台Windows,一台Linux)的设备也可以共享一套鼠标键盘。

需要注意的是所有设备必须处于`同一个局域网`内。

## 安装

### Windows

Winodws下安装很简单，直接下载这个[安装包](https://github.com/debauchee/barrier/releases)安装即可。

### Linux

各大发行版一般都有对应的包，例如Ubuntu可以直接使用`apt`安装：

```bash
sudo apt install barrier
```

## 使用说明

这个软件有两种模式，一种是服务端模式，一种是客户端模式。使用的时候需要一台设备充当服务端，其他的设备充当客户端, 启动服务端之后, 客户端只需要输入服务端的IP地址连接即可, 非常简单。

使用过程中需要注意的点：

### 0. 作者只尝试过使用Windows作为服务端，Linux作为客户端的情况

这里贴一个官方repo里面某个issue的连接，里面解决了很多问题，可以参考一下：
<https://github.com/debauchee/barrier/issues/190>

### 1. 网络问题，服务端和客户端必须要在一个局域网内，不能跨网段

启动服务端和客户端之后，可以通过barrier->日志查看日志消息，根据错误提示判断问题类型

```bash
# windows cmd下可以通过下面的命令查看ip地址, 也可以通过图形界面右下角点击所连接网络（有线或者无线）的属性查看
ipconfig
# linux下可以通过下面的命令查看ip地址
ip addr

# 可以通过下面的命令检查客户端和服务器是否可以建立TCP连接
# 服务端起一个http服务器
python3 -m http.server 8000
# 客户端访问服务端的http服务器
nc -vz 服务器ip地址 8000
# 如果可以建立连接，会输出下面的信息
Connection to 服务器ip地址 8000 port [tcp/*] succeeded!
```

### 2. 服务端多IP问题

使用的时候需要在客户端输入服务端的IP地址才能连接，如果出现了多个网络接口的ip地址，往往是Virtual box或者VMware的虚拟网卡，需要去掉这些虚拟网卡(禁用相关的网络适配器即可)，只保留真实的网卡，需要注意的是服务端会显示若干个网络接口地址，加黑的ip地址需要和真正的网卡地址(也就是你正在用的局域网分配给你的地址)一致

可以在Windows上启动一个http服务器测试网络的连通性

``` python
# Windows
python3 -m http.server 8000

# 然后在Linux上使用下面的命令查看是否可以访问
nc -vz 服务器ip地址 8000
```

### 3. 去掉SSL选项

依次点击Barrier->更改设置->开启SSL->去掉SSL选项

![去掉SSL选项](/imgs/ssl.png)

### 4. 关闭Windows防火墙

Windows设置->更新和安全->Windows安全中心->防火墙和网络保护

如下图所示

![关闭Win防火墙](/imgs/firewall.png)

域网络、专用网络、公用网络都需要关闭(实际上只用关闭公用网络就可以了，也就是用黄色标出来的正在使用的网络)

### 5. 注意查看日志

左上角barrier->日志选项，可以查看日志，根据日志提示解决问题，服务器和客户端都可以查看日志

```bash
# 在服务端启动后，可以通过下面的命令(如果在服务端输入可以检查是否barrier服务器是否成功启动，如果在客户端输入可以检测网络的连通性)检查客户端和服务器是否可以建立TCP连接, 其中24800是barrier默认的端口
nv -vz 服务器ip地址 24800

# 如果可以建立连接，会输出下面的信息
Connection to 服务器ip地址 24800 port [tcp/*] succeeded!
```

### 6. 服务端可以调整不同机器的逻辑布局

这个应该自己能找到

### 7. 修改Linux配置(这个好像没啥用？)

Linux配置忘了，好像不是很重要以后再说。。。

### 8. 鼠标停滞在客户端屏幕边缘的问题

[这个问题](https://github.com/debauchee/barrier/issues/206#issuecomment-962638647)是因为客户端的屏幕分辨率比服务端的屏幕分辨率低，导致鼠标停滞在客户端屏幕边缘

解决方法：

0. 服务端使用2.3.4的版本 参考这个: https://github.com/debauchee/barrier/issues/206#issuecomment-962638647
1. 可以通过修改客户端的分辨率或者缩放比例
