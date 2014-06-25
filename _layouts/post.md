---
layout: default
---
<h3 class="post-title">{{ page.title }}</h3>
<div class="post-content">
{{ content }}
</div>
<div class="post-time-line">
  <time datetime="{{ page.date | date:"%Y-%m-%d" }}">{{ page.date | date:"%Y-%m-%d" }}</time>
</div>
{% include comments.md %}