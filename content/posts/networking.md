---
title: "网络"
date: 2023-08-20T17:45:18+08:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["linux", "networking"]
author: "mkx"
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: "描述这篇文章."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## 1. Linux网络问题排查

### 1.1 iptables

[参考链接](https://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/)

iptables is a command-line firewall utility that uses policy chains to allow or block traffic. When a connection tries to establish itself on your system, iptables looks for a rule in its list to match it to. If it doesn't find one, it resorts to the default action.

You want to be **extremely careful** when configuring iptables rules, particularly if you're SSH'd into a server, because **one wrong command can permanently lock you out until it's manually fixed at the physical machine.**

ufw 是一个简单的防火墙应用程序，它是 iptables 的前端, 使用ufw命令就是在更新iptables。ufw 的目标是使防火墙配置变得简单，而不是简单化 iptables。

如果linux网络出现了问题，首先要检查iptables是否有规则限制了网络流量。

```bash
# 查看iptables规则
sudo iptables -vnL
# 允许所有流量
sudo iptables -P INPUT ACCEPT 
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
# 禁止所有流量(下面的命令会阻断所有网络流量，包括ssh连接，要慎用)
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT DROP
# 最重要的, 重置规则
sudo iptables -F
```

## 1.2 端口与netstat nmap nc telnet ss 命令

### 1.2.1 端口

[参考链接](https://www.digitalocean.com/community/tutorials/opening-a-port-on-linux)

Typically, ports identify a specific network service assigned to them. This can be changed by manually configuring the service to use a different port, but in general, the defaults can be used.

The first 1024 ports (port numbers 0 to 1023) are referred to as well-known port numbers and are reserved for the most commonly used services. These include SSH (port 22), HTTP (port 80), HTTPS (port 443).

### 1.2.2 netstat 等命令

```bash
# 列出所有正在监听的进程使用的ip和port
netstat -lntu
# or
ss -lntu

# 列出一些常用命令
telnet  {{host}} {{port}}
nc -zv {{host}} {{port}}
nmap -p {{port}} {{host}}
namp {{host}}
```
