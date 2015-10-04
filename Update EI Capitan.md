title: 升级 EI Capitan 碰到的一些问题
tags:
	- OS X
	- EI Capitan
categories:
	- Mac
date: 2015-10-04 22:17:57
---

昨天一晚上才下载升级好 EI Capitan，然而出现了点小问题。

1. 首先是左划的页面没有了，上面有好多好多stickies T.T 
		
		之前一直没注意，其实左划就是一个Dashboard而已，Launchpad里面打开就好了
		以及安利那个插件：Toggle Alfred，还是感觉比SpotLight好用
2. 然后是pod install没用了，提示command not found

		觉得ruby升级造成了，重新gem install cocoapods，结果给我报一堆错。各种莫名其妙的权限问题。
		用sudo su，结果报Connection reset by peer - SSL_connect，差点以为是阿里的那个ruby源有问题。
		结果，用这个解决了：sudo gem install -n /usr/local/bin cocoapods
3. 拖动微信窗口的时候有问题，各种跳闪。
4. 我写了这么多主要是因为不想再看mongodb的geo了。:)
5. 然而还是得看。