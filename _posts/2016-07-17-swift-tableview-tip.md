---
layout: post
title: "UITableView 小技巧"
description: ""
category: Swift
tags: ["UITableView"]
published: true
---

## 环境

*   使用 Swift 2.3

## 代码

设置分割线颜色

<pre><code class="language-swift">self.tableView.separatorColor = UIColor.redColor()
</code></pre>

设置背景颜色

<pre><code class="language-swift">self.tableView.backgroundColor = UIColor.redColor()
</code></pre>

Plain 样式去掉多余分割线

<pre><code class="language-swift">let tableFooterView = UIView()
tableFooterView.backgroundColor = UIColor.clearColor()
self.tableView.tableFooterView = tableFooterView
</code></pre>

Grouped 样式去掉顶部多余部分

<pre><code class="language-swift">self.tableView.tableHeaderView = UIView(frame: CGRectMake(0, 0, self.view.frame.size.width, 15))
self.tableView.contentInset = UIEdgeInsetsMake(-16, 0, 0, 0)
</code></pre>