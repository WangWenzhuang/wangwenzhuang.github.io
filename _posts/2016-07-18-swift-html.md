---
layout: post
title: "[ Swfit ] UILabel 显示 HTML"
description: ""
category: Swfit
tags: ["UILabel","HTML"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

## 代码

设置分割线颜色

```swift
// label 是 UILabel
let html = "&lt;html&gt;&lt;body&gt;&lt;p style=&#x27;text-align:center;&#x27;&gt;&lt;span style=&#x27;font-size:16px;color:#707070;&#x27;&gt;哈哈哈哈&lt;/span&gt;&lt;/p&gt;&lt;/body&gt;&lt;/html&gt;"
do {
    try label.attributedText = NSAttributedString(data: html.data(using: String.Encoding.unicode)!, options: [ NSDocumentTypeDocumentAttribute: NSHTMLTextDocumentType ], documentAttributes: nil)
} catch {
}
```