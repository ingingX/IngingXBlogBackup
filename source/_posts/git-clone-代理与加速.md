---
title: git 代理配置与 git clone 下载加速
top: false
cover: false
toc: true
mathjax: true
date: 2020-02-26 20:52:27
password:
summary: 解决 `git clone` 下载、GitHub 网页打开慢的问题；以及讨论一下git中如何配置代理服务器。
tags: Git
category: Tech Skills
---
Topics: 解决 `git clone` 下载、GitHub 网页打开慢的问题；以及讨论一下git中如何配置代理服务器。

Notes: 此文将介绍两种方法解决墙内 `git clone` 下载慢的问题。其中方法一在本文发出时（2020-02-26）测试无效，但去年（2019年）测试有效；方法二需要使用 ssr 或 v2ray 代理，请尝试前确定您可以在使用代理的情况下打开[谷歌搜索](www.google.com)。

## 1. 修改 `host` 文件以加速 `git clone` 和 GitHub 访问 

### steps:

在 [ip 查询网页](https://www.ipip.net/ip.html) 查询以下几个网址的当前 IP 地址：

```
github.global.ssl.fastly.Net
github.com
```

其中，第一个在 GitHub 上 clone 时的下载服务器地址，第二个是 GitHub 官网地址。

由于本地 IP 不同，所以每个人查询到的 GitHub 访问 IP 也不同。我查询出来是：

```
199.59.148.140
13.229.188.59
```
记录下这几个 IP， 去 host 文件，右键使用记事本打开：C:\Windows\System32\drivers\etc\hosts

在 host 文件末尾添加：

```
github.global.ssl.fastly.Net 199.59.148.140
github.com 13.229.188.59
```
最后使用命令提示符刷新 DNS 缓存，让计算机每次访问以上两个网址的时候都是用我们设定的 IP 访问 （这样理论上就可以避免被墙）：

``` bash
$ ipconfig /flushdns
```

### notes:

之前博主也是使用这种办法加速 `git clone`，但是最近似乎墙更高了，在两台电脑上测试了多次都无法加速。如果有大佬知道其中缘由或者可以改进还望不吝赐教。

## 2. 通过修改 Git 本身的配置以加速 `git clone`

### steps:

连接你的 vpn，设置为“全局代理模式”。可以通过尝试打开[谷歌搜索](www.google.com)来测试是否连接成功。

找到 vpn 的本地代理端口（一般是1080，但是也可能是其他的），我这里使用的是1080。

打开命令提示符，查看 Git 的的配置：

``` bash
$ git config -l
```

确认你的配置列表里没有 `https.proxy`，`http.proxy` 等带有 `proxy` 的配置。如果有，请参照本文下一部分（3）中的“取消代理设置”将之取消。

如果你使用 ssr 代理（socks5 协议），则输入：

``` bash
$ git config --global http.proxy socks5://127.0.0.1:1080
$ git config --global https.proxy socks5://127.0.0.1:1080
```

配置所有 Git 的网络访问都通过代理完成；

如果你使用 v2ray 代理（http/https 协议），则输入：

``` bash
$ git config --global http.proxy http://127.0.0.1:1080
$ git config --global https.proxy https://127.0.0.1:1080
```

### notes:

这个方法需要使用 ssr 或 v2ray 等 vpn 代理，这通常需要付费租用代理服务器或者购买节点。但好处是比较稳定，只要代理没有问题，Git 就可以满带宽下载（unlike 方法1，花钱才能变强）。博主目前使用了3个月，没有出现任何问题。

## 3. Git 的代理配置和一些思考

在命令提示符，可以查看 Git 的的配置：

``` bash
$ git config -l
```

![](/image/gitConfig.png)

其中，最后两行就是我们刚设置的代理。

如果想要恢复某个设置为初始值，可以这样：

``` bash
$ git config --global --unset [configName]
```

比如，想要取消刚才设置的代理：

``` bash
$ git config --global --unset http.proxy
$ git config --global --unset https.proxy
```

看一下 `git config -l`，是不是就没有代理的那个变量了？

### notes:

Git 是强大的工具，想用好它绝不是几个命令就ok的。通常使用的命令大约有10-20个，要精通则需要熟练至少50个相关的命令以及搞懂各个部分的功能和组成结构。