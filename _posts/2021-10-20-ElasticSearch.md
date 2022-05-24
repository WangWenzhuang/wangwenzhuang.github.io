---
layout: post
title: "ElasticSearch"
description: ""
category: 技术
tags: ["ElasticSearch"]
published: true
---

> 分布式全文搜索引擎框架，适用于近实时的搜索，1秒以内。本身就是一个 NOSQL 数据库，只不过存储的是索引数据。

## 特点

- API 以 RESTful 风格暴露，以 JSON 的方式请求和响应
- 在生产环境使用集群方式部署，开发使用单机部署
- 非常消耗内存

## 术语

- Index 索引库
- Type 类型（表）
- Document 一条记录
- Mapping 字段

## Docker 安装

需要下载中文分词器，**elasticsearch-analysis-ik**，地址：[https://github.com/medcl/elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)，需要注意，版本号要和 ES 一致，修改文件夹名字为 **analysis-ik**，拷贝到 **plugins** 文件夹中

docker-compose.yml

```yaml
version: '3'

services:
  elasticsearch:
    container_name: elasticsearch
    image: docker.elastic.co/elasticsearch/elasticsearch:5.6.8
    restart: always
    volumes:
      - ./config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml
      - ./data:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
      - "9300:9300"
    environment:
      ES_JAVA_OPTS: "-Xmx512m -Xms512m"
      ELASTIC_PASSWORD: changeme
      # Use single node discovery in order to disable production mode and avoid bootstrap checks
      # see https://www.elastic.co/guide/en/elasticsearch/reference/current/bootstrap-checks.html
      discovery.type: single-node
```

配置文件 elasticsearch.yml

```yaml
http.host: 0.0.0.0

http.cors.enabled: true
http.cors.allow-origin: "*"
```

启动

```bash
docker-compose up -d
```

## 可视化工具

使用 Google Chrome 插件，插件地址：[https://chrome.google.com/webstore/detail/elasticsearch-head/ffmkiejjmecolpfloofpjologoblkegm](https://chrome.google.com/webstore/detail/elasticsearch-head/ffmkiejjmecolpfloofpjologoblkegm)

## 知识点

### elasticsearch-analysis-ik 有两种分词策略

- **ik_smart** 智能分词
- **ik_max_word** 最细粒度分词

### 查询的两种方式

- **query_string** 搜索关键字会进行分词
- **term** 搜索关键字不进行分词

### 分片

默认5个分片，5个副本分片，一共是10个

## JAVA 操作

使用 **Spring Data Elasticsearch** 操作

## 集群的优点

> 高可用、容错性

- 单点故障，如果一台服务器挂掉，搜索服务就会挂
- 横向扩容，一台服务器的储存的索引数据是有限的，使用集群可以在线扩容
- 数据冗余，多台服务器可以冗余索引数据，备份

## 如何解决高并发

分布式的全文搜索引擎框架，隐藏了复杂的处理机制，内部使用分片机制、集群发现、分片负载均衡请求路由。

## 集群节点

- 主节点可以创建删除索引，并分配数据分片到相关节点
- 数据节点可以对文档进行增删改查、聚合操作