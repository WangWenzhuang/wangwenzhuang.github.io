---
layout: default
title: "UITableView 小技巧"
description: ""
tags: ["iOS"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

## 代码

设置分割线颜色

```swift
self.tableView.separatorColor = UIColor.red()
```

设置背景颜色

```swift
self.tableView.backgroundColor = UIColor.red()
```

Plain 样式去掉多余分割线

```swift
let tableFooterView = UIView()
tableFooterView.backgroundColor = UIColor.clear
self.tableView.tableFooterView = tableFooterView
```

Grouped 样式去掉顶部多余部分

```swift
self.tableView.tableHeaderView = UIView(frame: CGRect(x: 0, y: 0, width: self.view.frame.size.width, height: 15))
self.tableView.contentInset = UIEdgeInsetsMake(-16, 0, 0, 0)
```

去掉分割线左边空白（x=0）

```swift
override func tableView(_ tableView: UITableView, willDisplay cell: UITableViewCell, forRowAt indexPath: IndexPath) {
    cell.separatorInset = .zero
    cell.layoutMargins = .zero
}
```