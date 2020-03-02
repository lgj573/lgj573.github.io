---
layout: post
title: css选择器中:first-child与:first-of-type的区别
category: 前端
tags: [ionic , first-child , first-of-type]
description: css选择器中:first-child与:first-of-type的区别
---
 

# css选择器中:first-child与:first-of-type的区别


:first-child选择器是css2中定义的选择器，从字面意思上来看也很好理解，就是第一个子元素。比如有段代码：

 ```
 <div>
	<p>第一个子元素</p>
	<h1>第二个子元素</h1>
	<span>第三个子元素</span>
	<span>第四个子元素</span>
	
 </div>
 ```

p:first-child  匹配到的是p元素,因为p元素是div的第一个子元素；

h1:first-child  匹配不到任何元素，因为在这里h1是div的第二个子元素，而不是第一个；

span:first-child  匹配不到任何元素，因为在这里两个span元素都不是div的第一个子元素；

:first-child  匹配到的是p元素,因为在这里div的第一个子元素就是p。

 

然后，在css3中又定义了:first-of-type这个选择器，这个跟:first-child有什么区别呢？还是看那段代码：
 ```
 <div>
	<p>第一个子元素</p>
	<h1>第二个子元素</h1>
	<span>第三个子元素</span>
	<span>第四个子元素</span>
	
 </div>
 ```
 

p:first-of-type  匹配到的是p元素,因为p是div的所有为p的子元素中的第一个，事实上这里也只有一个为p的子元素；

h1:first-of-type  匹配到的是h1元素，因为h1是div的所有为h1的子元素中的第一个，事实上这里也只有一个为h1的子元素；

span:first-of-type  匹配到的是第三个子元素span。这里div有两个为span的子元素，匹配到的是第一个。

:first-of-type  匹配到的是p元素

 

所以，通过以上两个例子可以得出结论：

:first-child 匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素。

:first-of-type 匹配的是该类型的第一个，类型是指什么呢，就是冒号前面匹配到的东西，比如 p:first-of-type，就是指所有p元素中的第一个。这里不再限制是第一个子元素了，只要是该类型元素的第一个就行了，当然这些元素的范围都是属于同一级的，也就是同辈的。

同样类型的选择器 :last-child  和 :last-of-type、:nth-child(n)  和  :nth-of-type(n) 也可以这样去理解。

文章乃参考、转载其他博客所得，仅供自己学习作笔记使用！！！