---
layout: post
title: "[ Java ] Spring Boot 环境切换"
description: ""
category: Java
tags: ["Spring Boot"]
published: true
---

## 前言

> 在开发时，配置文件一般区分开发环境、测试环境和生产环境。针对不同环境有不同的配置，例如：生产环境的api地址和测试环境的api地址不同等。这时候一般都是每个环境有一个配置文件，在发布时根据环境选择对应的配置文件即可。在 Asp.Net Mvc 中使用 **Web.config**（开发）、**Web.Debug.config**（测试）、**Web.Release.config**（生产）文件用于区分环境。在 Spring Boot 中可以通过配置 **application.properties** 实现。

## pom.xml 配置

> profile可以让我们定义一系列的配置信息，然后指定其激活条件。这样我们就可以定义多个profile，然后每个profile对应不同的激活条件和配置信息，从而达到不同环境使用不同配置信息的效果。

### 配置 profile

```xml
<profiles>
    <profile>
        <id>test</id>
        <properties>
            <environment>test</environment>
        </properties>
    </profile>
    <profile>
        <id>prod</id>
        <properties>
            <environment>prod</environment>
        </properties>
    </profile>
</profiles>
```

以上代码定义了两种环境：test是测试环境，prod是生产环境

### 配置 resource

```xml
<resources>
    <resource>
        <filtering>true</filtering>
        <directory>src/main/resources</directory>
        <excludes>
            <exclude>application-test.properties</exclude>
            <exclude>application-prod.properties</exclude>
            <exclude>application.properties</exclude>
        </excludes>
    </resource>
    <resource>
        <filtering>true</filtering>
        <directory>src/main/resources</directory>
        <includes>
            <include>application-${environment}.properties</include>
            <include>application.properties</include>
        </includes>
    </resource>
</resources>
```

以上代码很好理解，**application-test.properties** 是测试环境的配置文件，**application-prod.properties** 是生产环境的配置文件。**${environment}** 是在发布时打包传入的参数，通过此参数切换配置文件

## application.properties 配置

配置打包时传入的参数

```bash
spring.profiles.active = @environment@
```

## mven 打包环境切换

```bash
mvn clean package -Dmaven.test.skip=true -P [environment]
```

**environment** 是传入的参数，例如生产环境命令

```bash
mvn clean package -Dmaven.test.skip=true -P prod
```

此时打包是使用的 **application-prod.properties** 文件