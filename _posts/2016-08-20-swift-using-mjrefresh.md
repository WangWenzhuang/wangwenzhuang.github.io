---
layout: post
title: "Swift 使用 MJRefresh"
description: "Swift 使用 MJRefresh"
category: 技术
tags: ["Swfit","MJRefresh"]
published: true
---

#### 环境 ####

*	使用 Swift 2.3

*	MJRefresh 3.1.12，[MJRefresh - GitHub](https://github.com/CoderMJLee/MJRefresh)

#### 代码 ####

<pre><code class="language-swift">let header = MJRefreshNormalHeader()
header.setRefreshingTarget(self, refreshingAction: Selector("headerRefresh"))
header.lastUpdatedTimeLabel.hidden = true
tableView.mj_header = header
tableView.mj_header.automaticallyChangeAlpha = true
let footer = MJRefreshBackNormalFooter()
footer.setRefreshingTarget(self, refreshingAction: Selector("footerRefresh"))
tableView.mj_footer = footer
// 执行刷新
tableView.mj_header.beginRefreshing()

// 停止下拉刷新
tableView.mj_header.endRefreshing()

// 停止上拉加载
tableView.mj_footer.endRefreshing()

// 设置上拉没有更多
tableView.mj_footer.endRefreshingWithNoMoreData()

// 重置没有更多
tableView.mj_footer.resetNoMoreData()
</code></pre>