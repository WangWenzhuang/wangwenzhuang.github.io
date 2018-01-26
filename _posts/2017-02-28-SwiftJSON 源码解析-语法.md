---
layout: post
title: "SwiftJSON 源码解析-语法"
description: ""
category: Swift
tags: ["SwiftJSON"]
published: true
---

## 简介

> SwiftyJSON 是 Swift 语言开发的一套 JSON 解析框架。SwiftJSON 使用简洁的语法解析 JSON，并为我们解决了可恶的 Optional（可选值），相信使用 Swift 进行开发的人对此深恶痛绝了。[GitHub 地址](https://github.com/SwiftyJSON/SwiftyJSON)

SwiftJSON 的源码都在 **SwiftyJSON.swift** 文件中，其中只有一个 **struct** **JSON**。为了更好的学习作者的思想，我认为需要先理解各种语法

### 为函数参数指定默认值

```swift
public init(data: Data, options opt: JSONSerialization.ReadingOptions = .allowFragments, error: NSErrorPointer = nil) {
}
```

这段代码中的 **options opt: JSONSerialization.ReadingOptions = .allowFragments** 就是将 **opt** 赋予默认值 **allowFragments**。默认值的优点是，指定默认值的参数可以不传参数。例如：**JSON(data: Data())**

### 外部参数名

还是上段代码，其中 **options opt: JSONSerialization.ReadingOptions = .allowFragments** 中的 **options** 是外部参数名，用于调用时显示的特定的名称，便于代码阅读。在外部使用时的应该是这样的：**JSON(data: , options: , error: )**

### 异常捕捉

```swift
do {
    let object: Any = try JSONSerialization.jsonObject(with: data, options: opt)
    self.init(jsonObject: object)
} catch let aError as NSError {
    if error != nil {
        error?.pointee = aError
    }
    self.init(jsonObject: NSNull())
}
```

使用 **do{}** 包住可能出现异常的代码块，使用 **try** 关键字去执行可能出现异常的代码。**catch{}** 包住异常后的代码块

### 调用函数省略参数名

```swift
public init(_ object: Any) {}
```

_ 修饰的参数，在调用时可以简写为 **JSON("Swift")**，如果不使用 _ 为 **JSON(object: "Swift")**

### **@available** 声明类型的生命周期依赖于特定的平台和系统版本

```swift
@available(*, deprecated: 3.2, message: "Use instead `init(parseJSON: )`")
public static func parse(_ json: String) -> JSON {
    return json.data(using: String.Encoding.utf8)
        .flatMap { JSON(data: $0) } ?? JSON(NSNull())
}
```

此方法在所有平台 **3.2** 版本后，不建议使用。调用时方法会显示删除线

### **fileprivate** 声明在文件范围内可访问

```swift
fileprivate init(jsonObject: Any) {
    self.object = jsonObject
}
fileprivate var rawArray: [Any] = []
```

在 Swift 中，我们都习惯将相同功能的代码使用 **extension**，例如实现某个协议的代码，我们会使用 **extension**，这样非常利于代码的阅读。但是如果在 **extension** 中需要访问使用 **private** 修饰的函数或变量等，是访问不到的。所以需要使用 **fileprivate** 进行修饰，**fileprivate** 的可访问范围是当前文件，例子：

```swift
class A: NSObject {
    private let B = "Swift"
}
extension A {
    func C() {
        print(self.B)// 此时会报错，使用fileprivate修饰才能访问到B
    }
}
```

### **mutating** 修饰 **struct**、**enum** 中的函数

```swift
public mutating func merge(with other: JSON) throws {
    try self.merge(with: other, typecheck: true)
}
```

在 Swift 中 **struct**、**enum** 中是可以声明实例函数和类函数的，不过实例函数中是不可以修改值类型的属性，所以需要使用 **mutating** 进行修饰

### **throws** 可能抛出的函数

还是上一段代码，其中 **throws** 关键字代表此函数可能会抛出异常。在调用此函数时需要在函数前使用 **try** 关键字。例如：**let object: Any = try JSONSerialization.jsonObject(with: data, options: opt)**

### 使用 **throw** 抛出异常

```swift
throw NSError(domain: ErrorDomain, code: ErrorWrongType, userInfo: [NSLocalizedDescriptionKey: "Couldn't merge, because the JSONs differ in type on top level."])
```

### 实现的协议

* Comparable 运算符重载，实现此协议可以对实例进行比较

* Collection 自定义集合，其中 **subscript** 方法是实现 json[] 的主要方法

* Swift.ExpressibleByIntegerLiteral、Swift.ExpressibleByBooleanLiteral、Swift.ExpressibleByFloatLiteral、Swift.ExpressibleByDictionaryLiteral、Swift.ExpressibleByArrayLiteral、Swift.ExpressibleByNilLiteral、Swift.RawRepresentable、
这些协议是扩展构造函数，Swift.ExpressibleByIntegerLiteral 协议代表可以使用字符串进行初始化。其它协议看名字就可以知道了

* Swift.CustomStringConvertible、Swift.CustomDebugStringConvertible 自定义 **description** 和 **debugDescription** 值