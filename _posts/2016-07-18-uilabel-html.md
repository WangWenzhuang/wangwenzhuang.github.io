---
layout: post
title: "UILabel 显示 HTML"
description: "UILabel 显示 HTML"
category: 技术
tags: ["Swfit","UILabel","HTML"]
published: true
---

#### 环境 ####

*   使用 Swift 2.3

#### 代码 ####

*设置分割线颜色*

<pre><code class="language-swift">// label 是 UILabel
let html = "<html><body><p style='text-align:center;'><span style='font-size:16px;color:#707070;'>哈哈哈哈</span></p></body></html>"
do {
    try label.attributedText = NSAttributedString(data: html.dataUsingEncoding(NSUnicodeStringEncoding)!, options: [ NSDocumentTypeDocumentAttribute: NSHTMLTextDocumentType ], documentAttributes: nil)
} catch {
}
</code></pre>