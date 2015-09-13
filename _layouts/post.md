---
layout: default
---
<script type="text/javascript">
	$(function () {
		$('#nav1').addClass('active');
	});
</script>
<div class="container content">
	<h3 class="post-title">{{ page.title }}</h3>
	<div class="post-title-line"></div>
	<div class="post-content">
	{{ content }}
	</div>
	<div class="post-time-line">
		分类：<span class="post-time-line-categories">{{ page.categories }}</span>&nbsp;&nbsp;|&nbsp;&nbsp;
		标签：
		{% for tag in page.tags %}
			<span class="post-time-line-tag">{{ tag }}</span>
		{% endfor %}
		&nbsp;&nbsp;|&nbsp;&nbsp;
		<time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
	</div>
	{% include comments.md %}
</div>