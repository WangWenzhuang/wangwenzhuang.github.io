---
layout: default
---
<script>
	$(function () {
        $("#blog").css("color","#fc0");
	});
</script>
<div class="container">
	<div class="post-title"><span class="fa fa-bookmark post-title-logo"></span>&nbsp;{{ page.title }}</div>
	<div class="post-time">
		<span class="fa fa-calendar"></span>&nbsp;<time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
	</div>
	<div class="post-content">{{ content }}</div>
	<div class="post-footer">
		<span class="fa fa-folder"></span>&nbsp;
		<span class="post-footer-categories">{{ page.categories }}</span>&nbsp;&nbsp;&nbsp;&nbsp;
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