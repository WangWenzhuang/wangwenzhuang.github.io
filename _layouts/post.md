---
layout: default
---
<script>
	$(function () {
		$("#blog").css("color", "#fc0");
	});
</script>
<div class="container">
	<div class="post-title">
		{{ page.title }}
	</div>

	<div class="post-content">{{ content }}</div>

	<div class="post-footer">
		<span class="post-footer-time">
			<span class="fa fa-calendar"></span>&nbsp;
			<time datetime="{{ page.date | date:"%Y-%m-%d" }}">
				{{ page.date | date:"%Y-%m-%d" }}
			</time>
		</span>
		<span class="post-footer-categories">
			<span class="fa fa-folder"></span>&nbsp;
			{{ page.categories }}
		</span>
	</div>
</div>