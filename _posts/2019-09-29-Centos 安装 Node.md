---
layout: post
title: "Centos 安装 Node"
description: ""
category: 技术
tags: ["Centos", "Node"]
published: true
---

```bash
wget https://nodejs.org/dist/v12.16.1/node-v12.16.1-linux-x64.tar

tar xvf node-v12.16.1-linux-x64.tar

mv node-v12.16.1-linux-x64 /usr/local/nodejs

ln -s /usr/local/nodejs/bin/npm /usr/local/bin/

ln -s /usr/local/nodejs/bin/node /usr/local/bin/

npm config set registry https://registry.npm.taobao.org

npm install webpack -g

npm install -g vue-cli

npm install -g yarn

yarn config set registry https://registry.npm.taobao.org -g

yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g
```

