title: 第一篇
tags:
  - Linux
  - CentOS
  - Firewall
categories:
  - 乱七八糟
date: 2015-10-02 00:30:00
comments: true
---


总算是下定决心租了域名和服务器，本意是做Golang的一个练手项目，自己写一个blog。

然而，恩，最终用了hexo，Golang慢慢来吧。:|

租了Vultr的服务器，用CentOS6，感谢陈总、彭博的鼎力支持和吐槽以及好心提供的VPN。

被小坑了一把，Vultr提供的Linux系统自动开启了防火墙，栽了一天半才突然想起来。

具体症状：

* VPS部署以后，在VPS上直接通过curl指令，访问localhost:port是可以访问的。
* 远程ping服务器的IP地址可以ping通。
* 远程直接访问VPS的外网IP显示的是ERR_EMPTY_RESPONSE。

解决方案：

* 在iptables里面放行需要的端口，这里放行的是80端口。

		sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
		sudo service iptables save

### 接下来的事

* Feeling服务端继续完善。（纸飞机那个算法好像好复杂的样子）
* Go还任重道远，慢慢在看GoBlog的代码
* 许总推荐的UNIX 网络编程好贵买不起
* 到底什么时候能见到猪猪呢 T.T