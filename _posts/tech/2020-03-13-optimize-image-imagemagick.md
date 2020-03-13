---
layout: post
title: imagemagick 优化图片
category: 技术
tags: [ssh,sublinux]
description: imagemagick 优化图片
--- 


原文地址 https://zwbetz.com/optimize-images-and-reduce-page-load-times-with-imagemagick/

img-optimize.cmd

```

@echo off

set size=800x
set quality=85

if "%1" == "" (
    echo Please specify an absolute path
    exit /b 
) 

pushd %1
magick mogrify -format jpg *.png
magick mogrify -resize %size% *.jpg
magick mogrify -strip -quality %quality% *.jpg
popd
 

```
An example usage:
```
img-optimize.cmd C:\Users\winuser\Desktop\Pics
```
