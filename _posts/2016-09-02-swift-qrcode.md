---
layout: post
title: "Swift 生成二维码"
description: ""
category: Swfit
tags: ["二维码"]
published: true
---

## 效果图

<img src="/images/post/2016-09-02-swift-create-qrcodeimage/IMG_3229.PNG" style="width:320px;height:569px;" />

## 环境

*	使用 Swift 2.3

## 代码

核心代码

<pre><code class="language-swift">func createQRCodeImage(text: String, width: CGFloat) -> UIImage {
    let filter = CIFilter(name: "CIQRCodeGenerator")
    filter?.setDefaults()
    filter?.setValue(text.dataUsingEncoding(NSUTF8StringEncoding), forKey: "inputMessage")
    let ciImage = filter?.outputImage
    let bgImage = createNonInterpolatedUIImageFormCIImage(ciImage!, width: width)
    return bgImage
}

private func createNonInterpolatedUIImageFormCIImage(image: CIImage, width: CGFloat) -> UIImage {
    let extent: CGRect = CGRectIntegral(image.extent)
    let scale: CGFloat = min(width/CGRectGetWidth(extent), width/CGRectGetHeight(extent))
    let width = CGRectGetWidth(extent) * scale
    let height = CGRectGetHeight(extent) * scale
    let cs: CGColorSpaceRef = CGColorSpaceCreateDeviceGray()!
    let bitmapRef = CGBitmapContextCreate(nil, Int(width), Int(height), 8, 0, cs, 0)!
    let context = CIContext(options: nil)
    let bitmapImage: CGImageRef = context.createCGImage(image, fromRect: extent)
    
    CGContextSetInterpolationQuality(bitmapRef,  CGInterpolationQuality.None)
    CGContextScaleCTM(bitmapRef, scale, scale)
    CGContextDrawImage(bitmapRef, extent, bitmapImage)
    let scaledImage: CGImageRef = CGBitmapContextCreateImage(bitmapRef)!
    return UIImage(CGImage: scaledImage)
}
</code></pre>