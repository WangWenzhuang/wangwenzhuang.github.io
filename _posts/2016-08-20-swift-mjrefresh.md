---
layout: post
title: "使用 MJRefresh 下拉刷新"
description: ""
category: Swfit
tags: ["MJRefresh"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

* [MJRefresh 3.1.1 - GitHub](https://github.com/CoderMJLee/MJRefresh)

## 快速使用

```swift
let header = MJRefreshNormalHeader()
header.setRefreshingTarget(self, refreshingAction: Selector("headerRefresh"))
header.lastUpdatedTimeLabel.hidden = true
tableView.mj_header = header
tableView.mj_header.isAutomaticallyChangeAlpha = true
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
```