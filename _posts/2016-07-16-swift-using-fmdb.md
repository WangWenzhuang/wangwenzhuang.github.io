---
layout: post
title: "Swift 使用 FMDB"
description: "Swift 使用 FMDB"
category: 技术
tags: ["Swfit","FMDB"]
published: true
---

## 环境 ##

*   使用 Swift 2.3

*   FMDB 2.5，[FMDB - GitHub](https://github.com/ccgus/fmdb)

## 代码 ##

指定数据库

<pre><code class="language-swift">let db = FMDatabase(path: "路径")
</code></pre>

打开数据库

<pre><code class="language-swift">db.open()
</code></pre>

更新数据

>   insert、update、delete...等语句统一属于更新操作（executeUpdate）

<pre><code class="language-swift">// 创建表
db.executeUpdate("CREATE TABLE NewsCategory([key] varchar(32),[sort] integer,[value] varchar(500),[type] varchar(30),isFixed integer,isCme integer);", withArgumentsInArray: nil)
// 插入数据
db.executeUpdate("INSERT INTO [NewsCategory] VALUES ('0', 0, '最新资讯', '0', 1, 0);", withArgumentsInArray: nil)
// 更新数据
db.executeUpdate("UPDATE [NewsCategory] SET [value]='最热资讯' WHERE WHERE [key]='0';", withArgumentsInArray: nil)
// 删除数据
db.executeUpdate("DELETE FROM [NewsCategory]", withArgumentsInArray: nil)
</code></pre>

查询数据

<pre><code class="language-swift">let result = db.executeQuery("select * from [NewsCategory] order by [sort]", withArgumentsInArray: nil)
while result.next() {
    // result.stringForColumn("key")! 得到key列
    // result.intForColumn("isCme") 得到isCme列
}
</code></pre>

关闭数据库

<pre><code class="language-swift">db.close()
</code></pre>

扩展

<pre><code class="language-swift">import FMDB
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
</code></pre>