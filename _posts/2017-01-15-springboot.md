---
layout: post
title: "[ 技术 ] Spring Boot 快速入门"
description: ""
category: 技术
tags: ["Spring Boot"]
published: true
---

## 前言

> 公司 App 后台我是使用 .Net 开发的，公司整体技术已经转向 Java，所以我也准备学一学入门一下。我用了一周的时间将代码转为 Java，现将此过程学到的记录下来。

## @RequestMapping 路由映射

### Url 映射
RequestMapping 注解是用来映射 Url 的。可以放在类上，也可以放在方法上。为类映射：

```java
@RequestMapping("api/app")
public class AppController {
}
```

这样就将 **api/app** 映射到 **AppController** 类。方法的映射也是一样：

```java
@RequestMapping("AppIsAudit")
public Map AppIsAudit() {
    // 实现代码
}
```

如果类上添加了 Url 映射，类中的方法会继承类的 Url，上面的 **AppIsAudit** 方法如果在 **AppController** 类中，那么路径为：**api/app/AppIsAudit**。

### 多个 Url 映射

```java
@RequestMapping({"/", "Default", "Index"})
```

这样就将 **/**、**/Default**、**/Index** 映射到同一个方法中。

### 指定 Http 方法

```java
@RequestMapping(value = "AutoSaveTest", method = RequestMethod.POST)
```

### 指定多个 HTPP 方法

```java
@RequestMapping(value = "AutoSaveTest", method = {RequestMethod.POST, RequestMethod.GET})
```

### 忽略大小写

RequestMapping 路径是大小写敏感的，**@RequestMapping("AppIsAudit")** 使用 **AppIsAudit** 是可以请求到，但是使用 **appisaudit** 是请求不到的。忽略大小写

## 接口

### 请求方法

## 页面

## thymeleaf

### 布局

### 页面绑定

### JavaScript 绑定