---
layout: post
title: Windows 下使用 RunHiddenConsole 启动 nginx、php
category: 技术
tags: [ssh,sublinux]
description: Windows 下使用 RunHiddenConsole 启动 nginx、php
--- 


原文地址 [https://blog.csdn.net/johnnycode/article/details/40148171](https://blog.csdn.net/johnnycode/article/details/40148171)

RunHiddenConsole.exe的作用是在执行完命令行脚本后可以自动关闭脚本,而从脚本中开启的进程不被关闭。简单来说就是黑窗体（CMD命令窗体）不会显示，但CMD命令窗体中运行的程序不会被关闭，特别是一些会挂住必须显示命令窗体的命令还真不错，如 Tomcat、Php、Nginx等。
 


1、启动 Php 和 Nginx ，根据自己的环境设置 php_home 和 nginx_home ，然后保存为 .bat 文件件即可。

```

@echo off
set php_home=./php/php-5.6.1-nts-Win32-VC11-x64
set nginx_home=./nginx/nginx-1.7.4

REM Windows 下无效
REM set PHP_FCGI_CHILDREN=5

REM 每个进程处理的最大请求数，或设置为 Windows 环境变量
set PHP_FCGI_MAX_REQUESTS=1000

echo Starting PHP FastCGI...
RunHiddenConsole %php_home%/php-cgi.exe -b 127.0.0.1:9000 -c %php_home%/php.ini
 
echo Starting nginx...
RunHiddenConsole %nginx_home%/nginx.exe -p %nginx_home% 
 

```


2、关闭 Php 和 Nginx

```

@echo off
echo Stopping nginx...  
taskkill /F /IM nginx.exe > nul
echo Stopping PHP FastCGI...
taskkill /F /IM php-cgi.exe > nul
exit

```

RunHiddenConsole 下载地址 https://gist.github.com/maiorano84/2b1a40926f49a55f9afd

https://redmine.lighttpd.net/attachments/660/RunHiddenConsole.zip