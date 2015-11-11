---
layout: post
title: "iOS 编译 FFmpeg"
description: "iOS 下完美编译 FFmpeg"
category: 技术
tags: ["FFmpeg"]
published: true
---

#### 下载 gas-preprocessor ####

*	下载 gas-preprocessor：[https://github.com/libav/gas-preprocessor](https://github.com/libav/gas-preprocessor)

*	复制**gas-preprocessor.pl**到/usr/sbin下

*	修改文件权限：chmod 777 /usr/sbin/gas-preprocessor.pl

#### 安装 yasm ####

<pre><code class="language-bash">curl http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz >yasm.tar.gz

tar xzvf yasm.tar.gz

cd yasm-1.2.0

./configure

make

sudo make install</code></pre>

可以到[http://www.tortall.net/projects/yasm/releases](http://www.tortall.net/projects/yasm/releases)查看最新版本 ，将 **yasm-1.2.0.tar.gz** 替换即可

#### 下载 FFmpeg-iOS-build-script（编译脚本）####

*	下载 FFmpeg-iOS-build-script：[https://github.com/kewlbear/FFmpeg-iOS-build-script](https://github.com/kewlbear/FFmpeg-iOS-build-script)

*	执行 ./build-ffmpeg.sh（编译所有版本）

*	上条语句执行完毕执行 ./build-ffmpeg.sh lipo（将所有架构.a文件合并）

*	执行完上述命令，在 **FFmpeg-iOS-build-script** 文件夹下会生成 **FFmpeg-iOS** 文件夹，进入 **FFmpeg-iOS** 文件夹查看支持架构：lipo -info libavcodec.a

#### 使用 FFmpeg ####
*	需要引入的库：libz.dylib、libbz2.dylib、libiconv.dylib

*	将 **FFmpeg-iOS** 拖入到工程

*	设置 **Library Search Paths** 为“$(PROJECT_DIR)/项目名称/FFmpeg-iOS/lib    non-recursive”

*	设置 **Header Search Paths** 为“$(PROJECT_DIR)/项目名称/FFmpeg-iOS/include    non-recursive”

*	设置 **Always Search User Paths** 为“NO”

#### 事例下载 ####

这里有份使用 FFMPEG 播放视频的代码：[https://github.com/kolyvan/kxmovie](https://github.com/kolyvan/kxmovie)