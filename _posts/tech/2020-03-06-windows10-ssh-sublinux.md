---
layout: post
title: windows10 ssh到ubuntu子系统
category: 技术
tags: [ssh,sublinux]
description: windows10 ssh到ubuntu子系统
--- 

```

user$ sudo apt-get remove --purge openssh-server # First remove sshd with --purge option.
user$ sudo apt-get install openssh-server
user$ sudo vi /etc/ssh/sshd_config # ** Change Port from 22 to 2222. (Just in case MS-Windows is using port 22).
user$ sudo service ssh --full-restart
 

```
