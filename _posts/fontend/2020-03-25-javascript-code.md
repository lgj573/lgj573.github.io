---
layout: post
title: Javascript code
category: java
tags: [Javascript]
description: Javascript code
---

[Javascript 生成随机密码](https://stackoverflow.com/questions/9719570/generate-random-password-string-with-requirements-in-javascript/9719815)
```
var randomstring = Math.random().toString(36).slice(-8);
```

[最小的评级组件](https://zhuanlan.zhihu.com/p/33464317)
```
"★★★★★☆☆☆☆☆".slice(5 - num, 10 - num);
```