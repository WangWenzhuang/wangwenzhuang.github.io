---
layout: post
title: "[ Java ] Spring Boot 快速入门"
description: ""
category: Java
tags: ["Spring Boot"]
published: true
---

## 前言

> 公司 App 后台我是使用 Asp.Net Mvc 5 开发的，公司整体技术已经转向 Java，所以我也准备学一学入门一下。我用了一周的时间使用 Spring Boot 将后台迁移到 Java。现将此过程学到的记录下来，有些术语是使用微软那一套去理解的，不要纠结。

## @RequestMapping 路由映射

### Url 映射
RequestMapping 注解是用来映射 Url 的。可以放在类上，也可以放在方法上。为类映射：

```java
@RequestMapping("api/app")
public class AppController { }
```

这样就将 **api/app** 映射到 **AppController** 类。方法的映射也是一样：

```java
@RequestMapping("appIsAudit")
public Map appIsAudit() {
    // 实现代码
}
```

如果类上添加了 Url 映射，类中的方法会继承类的 Url，上面的 **appIsAudit** 方法如果在 **AppController** 类中，那么路径为：**api/app/appIsAudit**。

### 多个 Url 映射

```java
@RequestMapping({"/", "default", "index"})
```

这样就将 **/**、**/default**、**/index** 映射到同一个方法中。

### RESTful

```java
@RequestMapping("index/{userId}")
public String index(Model model, @PathVariable String userId) {
    // 实现代码
}
```

### 指定 HTPP 方法

```java
@RequestMapping(value = "autoSaveTest", method = RequestMethod.POST)
```

### 指定多个 HTPP 方法

```java
@RequestMapping(value = "autoSaveTest", method = {RequestMethod.POST, RequestMethod.GET})
```

### 忽略大小写

RequestMapping 路径是大小写敏感的，**@RequestMapping("appIsAudit")** 使用 **appIsAudit** 是可以请求到，但是使用 **Appisaudit** 是请求不到的。忽略大小写：

```java
@Configuration
public class WebConfig extends WebMvcConfigurerAdapter {
    @Override
    public void configurePathMatch(PathMatchConfigurer configurer) {
        AntPathMatcher matcher = new AntPathMatcher();
        matcher.setCaseSensitive(false);
        configurer.setPathMatcher(matcher);
    }
}
```

## Api接口

在类上添加 **@RestController** 注解即可

```java
@RestController
@RequestMapping("api/app")
public class AppController { }
```

## 页面

在类上添加 **@Controller** 注解即可

```java
@Controller
public class HomeController { }
```

## thymeleaf

> Thymeleaf 提供了一个用于整合 Spring MVC 的可选模块，在应用开发中，你可以使用 Thymeleaf 来完全代替 JSP，或其他模板引擎，如 Velocity、FreeMarker 等。Thymeleaf 的主要目标在于提供一种可被浏览器正确显示的、格式良好的模板创建方式，因此也可以用作静态建模。你可以使用它创建经过验证的 XML 与 HTML 模板。相对于编写逻辑或代码，开发者只需将标签属性添加到模板中即可。接下来，这些标签属性就会在 DOM（文档对象模型）上执行预先制定好的逻辑。

[thymeleaf 官网](http://www.thymeleaf.org)

### 使用 thymeleaf

pom.xml 文件 **dependencies** 添加

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

### 页面存放路径

src/main/resources/templates/

### 使用页面

在 **templates** 文件夹创建 **.html** 文件，在 **@Controller** 中返回对应的 **.html** 文件名即可。

index.html

```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <title>首页</title>
</head>
<body>
首页
</body>
</html>
```

HomeController.java

```java
@Controller
public class HomeController {
    @RequestMapping({"/","index"})
    public String index() {
        return "index";
    }
}
```

这样 **HomeController** 中的 **index** 方法就会和 **index.html** 绑定了。

### 使用布局

> 在开发中，很多页面的布局都是统一的，不一样的只是内容。例如网站的导航就是统一的。一般会把这些一致的部分提取出来做成公共的，使用时只需要引入布局界面。

布局页中使用 **layout:fragment** 定义，作为需要改变的内容区域，下面是布局页 **layout.html**

```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no"/>
    <link rel="apple-touch-icon" sizes="57x57" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="114x114" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="72x72" href="/images/apple-touch-icon-144.png"/>
    <link rel="apple-touch-icon" sizes="144x144" href="/images/apple-touch-icon-144.png"/>
    <link rel="icon" type="image/x-icon" href="/images/favicon.ico"/>
    <link rel="stylesheet" href="/bootstrap-3.3.7/css/bootstrap.min.css"/>
    <script src="/jquery-3.1.1.min.js"></script>
    <script src="/bootstrap-3.3.7/js/bootstrap.min.js"></script>
    <script src="/layer_mobile/layer.js"></script>
</head>
<body>
<div class="container" style="margin-top: 15px;">
    <!--定义改变等内容-->
    <div layout:fragment="content"></div>
</div>
</body>
</html>
```

引用布局页面使用 **layout:decorator** 定义，下面是 **index.html** 使用布局页

```html
<!--引用 layout 布局页-->
<html layout:decorator="layout">
<head>
    <title>医博士</title>
</head>
<div layout:fragment="content">
    <ul class="list-group">
        <li class="list-group-item" style="text-align:center;"><span class="glyphicon glyphicon-info-sign"></span>
            yiboshi App for java v1.0
        </li>
    </ul>
</div>
</html>
```

此时 **index.html** 会合并内容，完整内容为

```html
<!DOCTYPE html>
<html>
<head>
    <title>医博士</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no"/>
    <link rel="apple-touch-icon" sizes="57x57" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="114x114" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="72x72" href="/images/apple-touch-icon-144.png"/>
    <link rel="apple-touch-icon" sizes="144x144" href="/images/apple-touch-icon-144.png"/>
    <link rel="icon" type="image/x-icon" href="/images/favicon.ico"/>
    <link rel="stylesheet" href="/bootstrap-3.3.7/css/bootstrap.min.css"/>
    <script src="/jquery-3.1.1.min.js"></script>
    <script src="/bootstrap-3.3.7/js/bootstrap.min.js"></script>
    <script src="/layer_mobile/layer.js"></script>
</head>
<body>
<div class="container" style="margin-top: 15px;">
    <div>
        <ul class="list-group">
            <li class="list-group-item" style="text-align:center;"><span class="glyphicon glyphicon-info-sign"></span>
                yiboshi App for java v1.0
            </li>
        </ul>
    </div>
</div>
</body>
</html>
```

### 使用部件（代码片段）

部件页中使用 **th:fragment** 定义，下面是部件页 **wxPart.html**。 这段代码主要作用为在微信中隐藏微信菜单栏

```html
<script th:fragment="wxHideMenu">
    function onBridgeReady() {
        WeixinJSBridge.call('hideOptionMenu');
    }
    if (typeof WeixinJSBridge == "undefined") {
        if (document.addEventListener) {
            document.addEventListener('WeixinJSBridgeReady', onBridgeReady, false);
        } else if (document.attachEvent) {
            document.attachEvent('WeixinJSBridgeReady', onBridgeReady);
            document.attachEvent('onWeixinJSBridgeReady', onBridgeReady);
        }
    } else {
        onBridgeReady();
    }
</script>
```

引用部件页面使用 **th:include** 定义，下面是 **index.html** 使用部件页

```html
<html layout:decorator="layout">
<head>
    <title>医博士</title>
    <script th:include="wxPart :: wxHideMenu"></script>
</head>
<div layout:fragment="content">
    <ul class="list-group">
        <li class="list-group-item" style="text-align:center;"><span class="glyphicon glyphicon-info-sign"></span>
            yiboshi App for java v1.0
        </li>
    </ul>
</div>
</html>
```

此时 **index.html** 会合并内容，完整内容为

```html
<!DOCTYPE html>
<html>
<head>
    <title>医博士</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no"/>
    <link rel="apple-touch-icon" sizes="57x57" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="114x114" href="/images/apple-touch-icon-114.png"/>
    <link rel="apple-touch-icon" sizes="72x72" href="/images/apple-touch-icon-144.png"/>
    <link rel="apple-touch-icon" sizes="144x144" href="/images/apple-touch-icon-144.png"/>
    <link rel="icon" type="image/x-icon" href="/images/favicon.ico"/>
    <link rel="stylesheet" href="/bootstrap-3.3.7/css/bootstrap.min.css"/>
    <script src="/jquery-3.1.1.min.js"></script>
    <script src="/bootstrap-3.3.7/js/bootstrap.min.js"></script>
    <script src="/layer_mobile/layer.js"></script>
    <script th:fragment="wxHideMenu">
        function onBridgeReady() {
            WeixinJSBridge.call('hideOptionMenu');
        }
        if (typeof WeixinJSBridge == "undefined") {
            if (document.addEventListener) {
                document.addEventListener('WeixinJSBridgeReady', onBridgeReady, false);
            } else if (document.attachEvent) {
                document.attachEvent('WeixinJSBridgeReady', onBridgeReady);
                document.attachEvent('onWeixinJSBridgeReady', onBridgeReady);
            }
        } else {
            onBridgeReady();
        }
    </script>
</head>
<body>
<div class="container" style="margin-top: 15px;">
    <div>
        <ul class="list-group">
            <li class="list-group-item" style="text-align:center;"><span class="glyphicon glyphicon-info-sign"></span>
                yiboshi App for java v1.0
            </li>
        </ul>
    </div>
</div>
</body>
</html>
```

### 变量绑定

>后台和前台使用变量进行传值，后台使用 **Model.addAttribute** 方法添加变量，前台使用 **${变量}** 表达式读取值。

后台方法

```java
@RequestMapping({"/","Index"})
public String Index(Model model) {
    model.addAttribute("Msg", "yiboshi App for java v1.0");
    return "Index";
}
```

.html

```html
<!--读取 Msg 值-->
<span th:text="${Msg}"></span>
```

### JavaScript 变量绑定

如果在 JavaScript 中读取变量首先需要在 **script** 标签中添加 **th:inline="javascript"**。然后需要使用 `/*<![CDATA[*/JavaScript 代码/*]]>*/` 包裹 JavaScript 代码。读取变量值使用 `/*[[${变量}]]*/`

```html
<script th:inline="javascript">
    /*<![CDATA[*/
    var msg = /*[[${Msg}]]*/ "";
    /*]]>*/
</script>
```