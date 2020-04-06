---
layout: post
title: nginx、php 本地速度慢
category: 技术
tags: [ssh,sublinux]
description: nginx、php 本地速度慢
--- 


原文地址 [https://blog.csdn.net/johnnycode/article/details/40148171](https://blog.csdn.net/johnnycode/article/details/40148171)


运行环境

 - 操作系统：win10
 - php版本：5.6.31
 - nginx版本：1.12.2
 - apache版本：2.4
 - mysql版本：5.6.37 
 
 解决思路
 
出现问题后，一开始以为是thinkphp5框架渲染页面的时候慢，所以在网上搜索的时候搜索的关键词就是“thinkphp5加载页面慢”，网上的说法有很多，最多的是以下几种：
1、你把连接数据库的host从localhost更改成127.0.0.1，给出的解释为：

1）PHP5.3以上，如果是链接localhost，会检测是IPV4还是IPV6，所以会比较慢。

2）windows系统下localhost是先进行本地HOST解析，然后走TCP/IP协议进行连接，127.0.0.1直接使用TCP/IP协议进行连接。[这里可以参考下这篇文章 PHP连接本地数据库用localhost还是127.0.0.1？]
以上两种解释我都没有一一验证，感兴趣的朋友可以自己验证下。这里我选择都采纳，跟别人解释的话我就这样解释，哈哈

2、thinkphp5本身不慢，这也能怪到框架上去，也是醉了（这个答案就忽略不计）
主要就是上面两种说法，一般情况下，如果你连接数据库时使用的host是localhost的话，跟换成127.0.0.1的确会快不少，然而，我的本身就是127.0.0.1了，所以忽略。

后来我就将项目部署到阿里云服务器上，php环境和本地几乎是一毛一样的，然后发现，线上运行速度超级快，本地是秒级的，而线上是毫秒级的，相差很大，切换页面基本没什么感觉。这时候就尴尬了，于是我把关键词从“thinkphp5加载页面慢”改成“php本地执行慢”，下面是我遇到的大部分答案：

1、将apache或者nginx的日志文件清理下，太大了会影响运行速度。（我的本地日志本身就很少，pass）

2、将host文件中的#127.0.0.1 localhost前面的#号去掉。（已试，速度是稍微快了那么一丢丢，但是没什么根本解决倾向，采用）

3、将localhost改成127.0.0.1（这个答案同上，数据库连接相关了，pass）

4、直接使用127.0.0.1来访问（我试过了，本来我是用nginx来进行转发的，特地关了nginx，更改apache的httpd.conf，返现运行速度没有太大变化，pass）
 