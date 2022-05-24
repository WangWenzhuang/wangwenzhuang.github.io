---
layout: post
title: "Cocoapods 指定不同版本 Swift"
description: ""
category: 技术
tags: ["Cocoapods", "Swift"]
published: true
---

```bash
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '9.0'
inhibit_all_warnings!
use_frameworks!

target 'LingShiEduLive' do
    pod 'Then', '2.4.0'
    pod 'ZKCommon', '4.0'
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    if ['ZKCommon'].include? target.name
      target.build_configurations.each do |config|
        config.build_settings['SWIFT_VERSION'] = '4.0'
      end
    end
  end
end
```

