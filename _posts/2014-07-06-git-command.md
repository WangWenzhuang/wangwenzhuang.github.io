---
layout: post
title: "Git 常用命令"
description: "git 简单配置和 git 的常用命令。用于随时查阅。。。"
category: 技术
tags: ["Git"]
published: true
---

#### 初次运行的配置 ####

设置用户信息

<pre><code class="language-bash">git config --global user.name "WangWenzhuang"
git config --global user.email "1020304029@qq.com"
</code></pre>

查看配置信息列表

<pre><code class="language-bash">git config --list</code></pre>

查看单个配置信息

<pre><code class="language-bash">git config user.name</code></pre>

生成 SSH 公钥

<pre><code class="language-bash">
ssh-keygen
</code></pre>

#### 常用命令 ####

从远程仓库克隆

<pre><code class="language-bash">
clone git@github.com:WangWenzhuang/test.git
</code></pre>

查看状态

<pre><code class="language-bash">
git status
</code></pre>

添加文件

<pre><code class="language-bash">
git add filename
</code></pre>

删除文件

<pre><code class="language-bash">
git rm filename
</code></pre>

查看修改的内容

<pre><code class="language-bash">
git diff
</code></pre>

提交更新

<pre><code class="language-bash">
git commit -m "提交更新"
</code></pre>

查看提交历史

<pre><code class="language-bash">
git log
</code></pre>

查看远程仓库

<pre><code class="language-bash">
git remote
git remote -v
</code></pre>

拉取远程仓库数据[不会自动合并]

<pre><code class="language-bash">
git fetch git@github.com:wangwenzhuang/test.git
</code></pre>

拉取远程仓库数据[自动合并]

<pre><code class="language-bash">
git pull
</code></pre>

将更新推送到远程仓库

<pre><code class="language-bash">
git push
</code></pre>

#### 获取帮助 ####

<pre><code class="language-bash">
git help <verb>
</code></pre>

例如查看config使用

<pre><code class="language-bash">
git help config
</code></pre>