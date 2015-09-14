---
layout: default
---
<div class="container content">
	<h4 class="post-title">{{ page.title }}</h4>
	<div class="post-title-line"></div>
	<div class="post-content">
	{{ content }}
	</div>
	<div class="post-time-line">
		分类：<span class="post-time-line-categories">{{ page.categories }}</span>&nbsp;&nbsp;|&nbsp;&nbsp;
		<time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
	</div>
	{% include comments.md %}
</div>