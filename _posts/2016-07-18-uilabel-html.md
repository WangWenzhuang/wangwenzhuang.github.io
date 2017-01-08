---
layout: post
title: "UILabel 显示 HTML"
description: "UILabel 显示 HTML"
category: 技术
tags: ["Swfit","UILabel","HTML"]
published: true
---

## 环境

*   使用 Swift 2.3

## 代码

设置分割线颜色

<pre><code class="language-swift">// label 是 UILabel
let html = "&lt;html&gt;&lt;body&gt;&lt;p style=&#x27;text-align:center;&#x27;&gt;&lt;span style=&#x27;font-size:16px;color:#707070;&#x27;&gt;哈哈哈哈&lt;/span&gt;&lt;/p&gt;&lt;/body&gt;&lt;/html&gt;"
do {
    try label.attributedText = NSAttributedString(data: html.dataUsingEncoding(NSUnicodeStringEncoding)!, options: [ NSDocumentTypeDocumentAttribute: NSHTMLTextDocumentType ], documentAttributes: nil)
} catch {
}
</code></pre>