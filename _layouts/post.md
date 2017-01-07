---
layout: default
---
<div class="container">
	<div class="post-title">{{ page.title }}</div>
	<span class="fa fa-calendar"></span>&nbsp;日期：<time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
	<div class="post-content">{{ content }}</div>
	<div class="post-footer">
		<span class="fa fa-folder"></span>&nbsp;
		<span class="post-footer-categories">{{ page.categories }}</span>&nbsp;&nbsp;
		{% if page.tags != empty %}
			<span class="fa fa-tag"></span>&nbsp;
			{% for tag in page.tags %}
				<span class="post-footer-tags">{{ tag }}</span>
				{% if forloop.last == false %}、{%endif %}
			{% endfor %}
		{%endif %}
	</div>
	{% include comments.md %}
</div>