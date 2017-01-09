---
layout: post
title: "使用 DZNEmptyDataSet"
description: ""
category: Swfit
tags: ["DZNEmptyDataSet"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

* [DZNEmptyDataSet 1.8.1 - GitHub](https://github.com/dzenbot/DZNEmptyDataSet)

## 快速使用

实现 **DZNEmptyDataSetSource**、**DZNEmptyDataSetDelegate** 两个协议

设置代理

```swift
self.tableView.emptyDataSetSource = self
self.tableView.emptyDataSetDelegate = self
```

实现协议

```swift
func emptyDataSetShouldDisplay(_ scrollView: UIScrollView!) -> Bool {
    // 数据为空时是否显示
    return true
}

func emptyDataSetShouldAllowScroll(_ scrollView: UIScrollView!) -> Bool {
    // 数据为空时是否可以上下拉动
    return true
}

func image(forEmptyDataSet scrollView: UIScrollView!) -> UIImage! {
	// 数据为空时显示的图片
    return UIImage(named: "emptyData")
}

func title(forEmptyDataSet scrollView: UIScrollView!) -> NSAttributedString! {
	// 数据为空是显示的文字
    return NSAttributedString(string: "没有数据", attributes: [ NSFontAttributeName : UIFont(name: "HelveticaNeue", size: 17)!, NSForegroundColorAttributeName : UIColor.red() ])
}
```