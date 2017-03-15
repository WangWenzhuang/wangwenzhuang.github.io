---
layout: post
title: "[ Swfit ] 生成二维码"
description: ""
category: Swfit
tags: ["二维码"]
published: true
---

## 效果图

![demo](/images/post/2016-09-02-swift-qrcode/IMG_3229.PNG)

## 环境

* Swift 3.0.2

* Xcode 8.2.1

## 代码

核心代码

```swift
func createQRCodeImage(_ text: String, width: CGFloat) -> UIImage {
    let filter = CIFilter(name: "CIQRCodeGenerator")
    filter?.setDefaults()
    filter?.setValue(text.data(using: String.Encoding.utf8), forKey: "inputMessage")
    let ciImage = filter?.outputImage
    let bgImage = createNonInterpolatedUIImageFormCIImage(ciImage!, width: width)
    return bgImage
}

fileprivate func createNonInterpolatedUIImageFormCIImage(_ image: CIImage, width: CGFloat) -> UIImage {
    let extent: CGRect = image.extent.integral
    let scale: CGFloat = min(width/extent.width, width/extent.height)
    let width = extent.width * scale
    let height = extent.height * scale
    let cs: CGColorSpace = CGColorSpaceCreateDeviceGray()
    let bitmapRef = CGContext(data: nil, width: Int(width), height: Int(height), bitsPerComponent: 8, bytesPerRow: 0, space: cs, bitmapInfo: 0)!
    let context = CIContext(options: nil)
    let bitmapImage: CGImage = context.createCGImage(image, from: extent)!
    
    bitmapRef.interpolationQuality = CGInterpolationQuality.none
    bitmapRef.scaleBy(x: scale, y: scale)
    bitmapRef.draw(bitmapImage, in: extent)
    let scaledImage: CGImage = bitmapRef.makeImage()!
    return UIImage(cgImage: scaledImage)
}
```

使用

```swift
self.QRCodeImg.image = self.createQRCodeImage(data, width: UIScreen.main.bounds.size.width - UIScreen.main.bounds.size.width * 0.2)
```