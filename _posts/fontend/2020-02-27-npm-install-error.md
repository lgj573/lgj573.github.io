---
layout: post
title: npm install 错误
category: 前端
tags: [ionic , npm]
description: npm install 碰到的问题
---

# 尝试和选择

## 卡壳
 * 一开始卡在 npm install,error fetchMetadata: sill install loadAllDepsIntoIdealTree
 * 试了npm install node-sass --registry=http://registry.npm.taobao.org，不行
 
## 换registry
 * npm config set registry https://registry.npm.taobao.org
 * npm config get registry 显示是Taobao的registry
 * 还是不行
## 尝试 cnpm
 * npm install -g cnpm --registry=https://registry.npm.taobao.org
 * cnpm install
 * 出现错误 request to https://registry.npm.taobao.org/fstream failed, reason: Client network socket disconnected before secure TLS connection was established
## 升级node
 > 还是不行
## 重新设置proxy
 * npm config get proxy,显示是http://localhost:1080
 * 代理没有问题，前几天还好好的
 * 重置 npm config set proxy null
 * 问题解决

 