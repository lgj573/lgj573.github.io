---
layout: post
title: jQuery accordion
category: 前端
tags: [ionic , first-child , first-of-type]
description: jQuery accordion
---
  

原文地址 [https://codepen.io/johanmouchet/pen/jARwrK](https://codepen.io/johanmouchet/pen/jARwrK)
  [https://uicookies.com/jquery-accordion/](https://uicookies.com/jquery-accordion/)


html
 ```html
 <h1>jQuery accordion</h1>

<ul class="accordion">
	<li class="accordion-item is-active">
		<h3 class="accordion-thumb">Lorem ipsum</h3>
		<p class="accordion-panel">
			Lorem ipsum dolor sit amet, consectetur adipisicing
			elit. Placeat, quibusdam! Voluptate nobis, beatae
			tempora praesentium, illum quis illo, maiores quod
			similique placeat, saepe mollitia dolor officiis
			aspernatur deleniti debitis commodi!
		</p>
	</li>
	
	<li class="accordion-item">
		<h3 class="accordion-thumb">Dolor sit amet</h3>
		<p class="accordion-panel">
			Lorem ipsum dolor sit amet, consectetur adipisicing
			elit. Reprehenderit quos, accusamus! Enim labore totam
			dicta quibusdam? Eveniet quis asperiores reprehenderit
			eaque atque in iure voluptate, explicabo, placeat, id
			earum architecto!
		</p>
	</li>
	
	<li class="accordion-item">
		<h3 class="accordion-thumb">Consectetur adipisicing elit</h3>
		<p class="accordion-panel">
			Lorem ipsum dolor sit amet, consectetur adipisicing
			elit. Reprehenderit quos, accusamus! Enim labore
			totam dicta quibusdam? Eveniet quis asperiores
			reprehenderit eaque atque in iure voluptate,
			explicabo, placeat, id earum architecto!
		</p>
	</li>
</ul>
 ```

css
 ```
.accordion {
  margin: 1rem 0;
  padding: 0;
  list-style: none;
  border-top: 1px solid #e5e5e5;
}

.accordion-item {
  border-bottom: 1px solid #e5e5e5;
}

/* Thumb */
.accordion-thumb {
  margin: 0;
  padding: .8rem 0;
  cursor: pointer;
  font-weight: normal;
}
.accordion-thumb::before {
  content: '';
  display: inline-block;
  height: 7px;
  width: 7px;
  margin-right: 1rem;
  margin-left: .5rem;
  vertical-align: middle;
  border-right: 1px solid;
  border-bottom: 1px solid;
  -webkit-transform: rotate(-45deg);
          transform: rotate(-45deg);
  -webkit-transition: -webkit-transform .2s ease-out;
  transition: -webkit-transform .2s ease-out;
  transition: transform .2s ease-out;
  transition: transform .2s ease-out, -webkit-transform .2s ease-out;
}

/* Panel */
.accordion-panel {
  margin: 0;
  padding-bottom: .8rem;
  display: none;
}

/* Active */
.accordion-item.is-active .accordion-thumb::before {
  -webkit-transform: rotate(45deg);
          transform: rotate(45deg);
}

/* General page styling */
html {
  font-family: sans-serif;
  font-size: 14px;
  color: #444;
}

body {
  line-height: 1.5;
  margin: 0 auto;
  max-width: 500px;
}

h1 {
  font-family: serif;
  margin-top: 15%;
}

 ```
 
js
 ```
 $(function() {
	// (Optional) Active an item if it has the class "is-active"	
	$(".accordion > .accordion-item.is-active").children(".accordion-panel").slideDown();
	
	$(".accordion > .accordion-item").click(function() {
		// Cancel the siblings
		$(this).siblings(".accordion-item").removeClass("is-active").children(".accordion-panel").slideUp();
		// Toggle the item
		$(this).toggleClass("is-active").children(".accordion-panel").slideToggle("ease-out");
	});
});
  ```
 