---
layout: post
title: "使用 FMDB 操作数据库"
description: ""
category: Swfit
tags: ["FMDB"]
published: true
---

## 环境

* Swift 3.0.2

* Xcode 8.2.1

* [FMDB 2.6.2 - GitHub](https://github.com/ccgus/fmdb)

## 快速使用

指定数据库

```swift
let db = FMDatabase(path: "路径")
```

打开数据库

```swift
db?.open()
```

更新数据

> insert、update、delete...等语句统一属于更新操作（executeUpdate）

```swift
// 创建表
db.executeUpdate("CREATE TABLE NewsCategory([key] varchar(32),[sort] integer,[value] varchar(500),[type] varchar(30),isFixed integer,isCme integer);", withArgumentsInArray: nil)
// 插入数据
db.executeUpdate("INSERT INTO [NewsCategory] VALUES ('0', 0, '最新资讯', '0', 1, 0);", withArgumentsInArray: nil)
// 更新数据
db.executeUpdate("UPDATE [NewsCategory] SET [value]='最热资讯' WHERE WHERE [key]='0';", withArgumentsInArray: nil)
// 删除数据
db.executeUpdate("DELETE FROM [NewsCategory]", withArgumentsInArray: nil)
```

查询数据

```swift
let result = db.executeQuery("select * from [NewsCategory] order by [sort]", withArgumentsInArray: nil)
while result.next() {
    // result.stringForColumn("key")! 得到key列
    // result.intForColumn("isCme") 得到isCme列
}
```

关闭数据库

```swift
db.close()
```

## 扩展

```swift
import FMDB
extension FMDatabase {
    static func manager() -> FMDatabase {
        let db = FMDatabase(path: "路径")
        let isOpen = db.open()
        assert(isOpen, "打开数据库失败")
        return db
    }
}

// 使用
// let db = FMDatabase.manager()
```