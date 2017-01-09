---
layout: post
title: "ZKModel 功能强大的实体模型转换器"
description: ""
category: iOS
tags: ["ZKModel"]
published: true
---

## ZKModel

> ZKModel 是一个功能强大的实体模型转换器
[ZKModel - GitHub](https://github.com/WangWenzhuang/ZKModel)

## 安装

<pre><code class="language-bash">CocoaPods：pod 'ZKModel'</code></pre>

## 使用

实体类

* UserModel.h

    <pre><code class="language-objectivec">#import "ZKModel.h"

    @interface UserModel : ZKModel&lt;ZKModelSerializing&gt;
    /**
    *  对应数据表字段id，对应json字段id
    */
    @property(nonatomic, copy) NSString *key;
    /**
    *  对应数据表字段name，对应json字段name
    */
    @property(nonatomic, copy) NSString *name;
    /**
    *  对应数据表字段age，对应json字段
    */
    @property(nonatomic, copy) NSNumber *age;
    @end</code></pre>

* UserModel.m

    ```objc
    #import "UserModel.h"

    @implementation UserModel

    + (NSString *)ZKDBTableName {
        return @"User";
    }
    + (NSDictionary *)ZKDBPrimaryKeys {
        return @{ @"key" : @"id" };
    }
    + (NSDictionary *)ZKPropertyKeys {
        return @{
                @"key" : @"id",
                @"name" : @"name",
                @"age" : @"age"
                };
    }
    @end
    ```

示例

<pre><code class="language-objectivec">NSDictionary *userDic = @{ @"id" : @"1", @"name" : @"王文壮", @"age" : @30 };
// 将 NSDictionary 转换为 UserModel
UserModel *user = [ZKModelAdapter modelOfClass:[UserModel class] fromDictionary:userDic];

NSArray *userArray = @[
                        @{ @"id" : @"1", @"name" : @"王文壮", @"age" : @30 },
                        @{ @"id" : @"2", @"name" : @"壮文王", @"age" : @30 }
                        ];
// 将元素为 NSDictionary 的 NSArray 转换为元素为 UserModel 的 NSArray
NSArray *users = [ZKModelAdapter modelsOfClass:[UserModel class] fromArray:userArray];

// 将 UserModel 转换为 JSON
NSString *json = [ZKModelAdapter JSONOfModelClass:[UserModel class] fromModel:user];
NSLog(@"User JSON:%@", json);

// 将元素为 UserModel 的 NSArray 转换为 JSON
json = [ZKModelAdapter JSONOfModelArray:users];
NSLog(@"Users JSON:%@", json);

// 实体输出 JSON
json = [user toJSON];
NSLog(@"Users JSON:%@", json);

// 实体输出 NSDictionary
userDic = [user dictionry];</code></pre>

## 运行环境

*	iOS 7+
*	支持 armv7/armv7s/arm64