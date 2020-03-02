---
layout: post
title: mysql之char和varchar的区别
category: mysql
tags: [mysql , char]
description: mysql之char和varchar的区别
---

char和varchar都是用来存储字符串的，但是他们保持和检索的方式不同。

char是属于固定长度的字符类型，而varchar是属于可变长度的字符类型。

由于char是固定长度的所以它的处理速度比varchar快很多。但是缺点是浪费存储空间，读取char类型数据时候时如果尾部有空格会丢失空格，所以对于那种长度变化不大的并且对查询速度有较高要求的数据可以考虑使用char类型来存储。

另外随着MySQL版本的不断升级，varchar数据类型的性能也在不断改进并提高，所以在许多的应用中，varchar类型被更多的使用

不同的存储引擎对char和varchar的使用原则有所不同：

 - MyISAM存储引擎：建议使用固定长度的数据列代替可变长度的数据列。
 - MEMORY存储引擎：目前都使用固定长度的数据行存储，因此无论使用CHAR或VARCHAR列都没有关系。两者都是作为CHAR类型处理。
 - InnoDB存储引擎：建议使用VARCHAR类型。对于InnoDB数据表，内部的行存储格式没有区分固定长度和可变长度列（所有数据行都使用指向数据列值的头指针），因此在本质上，使用固定长度的CHAR列不一定比使用可变长度VARCHAR列性能要好。因而，主要的性能因素是数据行使用的存储总量。由于CHAR平均占用的空间多于VARCHAR，因此使用VARCHAR来最小化需要处理的数据行的存储总量和磁盘I/O是比较好的。