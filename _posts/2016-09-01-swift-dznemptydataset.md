---
layout: post
title: "Swift 使用 DZNEmptyDataSet"
description: ""
category: Swfit
tags: ["DZNEmptyDataSet"]
published: true
---

## 环境

*	使用 Swift 2.3

*	DZNEmptyDataSet 1.8.1，[DZNEmptyDataSet - GitHub](https://github.com/dzenbot/DZNEmptyDataSet)

## 代码

实现 **DZNEmptyDataSetSource**、**DZNEmptyDataSetDelegate** 两个协议

设置代理

<pre><code class="language-swift">self.tableView.emptyDataSetSource = self
self.tableView.emptyDataSetDelegate = self
</code></pre>

实现

<pre><code class="language-swift">func emptyDataSetShouldDisplay(scrollView: UIScrollView!) -> Bool {
	// 数据为空时是否显示
    return true
}

func emptyDataSetShouldAllowScroll(scrollView: UIScrollView!) -> Bool {
	// 数据为空时是否可以上下拉动
    return true
}

func imageForEmptyDataSet(scrollView: UIScrollView!) -> UIImage! {
	// 数据为空时显示的图片
    return UIImage(named: "emptyData")
}

func titleForEmptyDataSet(scrollView: UIScrollView!) -> NSAttributedString! {
	// 数据为空是显示的文字
    return NSAttributedString(
    string: "没有数据", 
    attributes: 
    	 [ NSFontAttributeName : UIFont(name: "HelveticaNeue", size: 17)!, 
    	 NSForegroundColorAttributeName : UIColor.redColor() ])
}
</code></pre>