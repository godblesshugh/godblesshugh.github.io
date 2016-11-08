---
layout: post
title: MQTT 协议实现框架 -- Surgemq
date: 2016-11-9 20:49:00
categories: Go MQTT
---
[我自己的github地址](https://github.com/godblesshugh/surgemq.git) fork from [influxdata/surgemq](https://github.com/influxdata/surgemq.git)

## 某些预先处理

### 更改 import 路径  
首先为了更好的做本地测试，将所有原仓库中
`github.com/surgemq/*`
更改为相对地址(定义在 gopath 中)
`surgemq/*`

### 防止出现大量预料之中的错误输出
让原有的判断是否到达数据流末尾重新生效，取消注销：
`if err != io.EOF {`

### 断开连接后，出现错误：use of closed network connection
问题可见：[issue](https://github.com/golang/go/issues/4373)
具体出现场景和原意相同，使用了一个已经关闭的网络连接，但是无法通过类似的逻辑判断出来：
`if err != io.EOF {`
是 golang 本身对 net/net.go 中定义的 opError 未公开，因此只能通过字符串判断方式来确定这个报错，解决方案可见：[PR](https://github.com/influxdata/surgemq/pull/46/commits/ab46e73d3e50f94d27702bdff99eda3520ecd6f9)

## 某些功能特性(待续)
[作者博客](http://zhen.org/)
[主要参照的文字](http://zhen.org/blog/surgemq-mqtt-message-queue-750k-mps/)
p.s. 写到这儿的时候在听[云巴张虎](http://zhang.hu/) 直播，他说开源的 MQTT  实现现在都不太好，达不到商用要求。sign
### 使用 ring buffer 来代替 chan
好处是可以用 peek 的方式来读取 net.Conn 中的内容来处理，避免进行大量的内存中数据拷贝，从而一定程度上解决效率问题
坏处是需要自己控制锁，po 主也是在上面踩了好多坑。

### 接下来准备改造 auth 模块，加入 OAuth 实现逻辑。