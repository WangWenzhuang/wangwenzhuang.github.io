---
layout: default
---
<div class="container">
	<div class="post-title">{{ page.title }}</div>
	<div class="post-content">{{ content }}</div>
	<div class="post-footer">
		分类：<span class="post-footer-categories">{{ page.categories }}</span>&nbsp;&nbsp;|&nbsp;&nbsp;
		{% if page.tags != empty %}
		<span class="fa fa-tag"></span>&nbsp;标签：
		{% for tag in page.tags %}
			{{ tag }}
		{% endfor %}
		{%endif %}
		<span class="fa fa-calendar"></span>&nbsp;<time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
	</div>
	{% include comments.md %}
</div>