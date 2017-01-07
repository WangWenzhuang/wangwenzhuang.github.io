---
layout: post
title: "ZKSegment 功能强大的分段选择控件"
description: "ZKSegment 是一个分段选择控件，支持多种样式选择，功能强大"
category: 技术
tags: ["ZKSegment"]
published: true
---

# ZKSegment #

ZKSegment 是一个分段选择控件，支持多种样式选择，功能强大

[ZKSegment - GitHub](https://github.com/WangWenzhuang/ZKSegment)

<img src="/images/post/2015-10-24-zksegment/1.png" style="width:320px;height:480px;" />

<img src="/images/post/2015-10-24-zksegment/2.png" style="width:320px;height:480px;" />

<img src="/images/post/2015-10-24-zksegment/3.png" style="width:320px;height:480px;" />

# 安装 #

<pre><code class="language-bash">CocoaPods：pod 'ZKSegment'</code></pre>

# 快速使用 #

<pre><code class="language-objectivec">_ZKSegment = [ZKSegment
    zk_segmentWithFrame:CGRectMake(0, 0, self.view.bounds.size.width, 45)
                  style:ZKSegmentLineStyle];
_ZKSegment.zk_itemClickBlock=^(NSString *itemName , NSInteger itemIndex){
    NSLog(@"click item:%@",itemName);
    NSLog(@"click itemIndex:%d",itemIndex);
};
[_ZKSegment zk_setItems:@[ @"菜单1", @"菜单2" ]];

[self.view addSubview:_ZKSegment];</code></pre>

# 自定义 #

<pre><code class="language-objectivec">zk_itemDefaultColor				\\设置每一项文本默认颜色

zk_itemStyleSelectedColor		\\设置每一项文本选中颜色

zk_itemStyleSelectedColor		\\选中项样式颜色

zk_backgroundColor				\\背景色</code></pre>

# 运行环境 #

*	iOS 7+
*	支持 armv7/armv7s/arm64