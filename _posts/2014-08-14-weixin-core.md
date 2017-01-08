---
layout: post
title: "微信公众号开发 SDK"
description: "开发语言是 C#，大部分功能已经实现，简单易用。如果需要看实现功能，可以扫描下面二维码，关注测试帐号。"
category: 技术
tags: ["微信公众号开发"]
published: true
---

## 说明

开发语言是 C#，大部分功能已经实现，简单易用。

[WeiXin - GitHub](https://github.com/WangWenzhuang/WeiXin)

## 快速使用

1、实现 IWeiXinService 接口

<pre><code class="language-csharp">// 首先实现 IWeiXinService 接口
public class ProcessMessage : IWeiXinService
{
    /// <summary>
    /// 处理消息的接口，如果回复被动消息，直接回复 xml 格式的消息即可。
    /// 如果不处理或者发送客服消息等直接回复空字符串即可。
    /// </summary>
    /// <param name="receiveXmlMsgType"></param>
    /// <param name="receiveXmlMessage"></param>
    /// <returns></returns>
    public string Process(ReceiveXmlMessageType receiveXmlMsgType, ReceiveXmlMessage receiveXmlMessage)
    {
        string result = string.Empty;
        if (receiveXmlMessage != null)
        {
            // 消息类型
            switch (receiveXmlMsgType)
            {
                case ReceiveXmlMessageType.Undefined:                          // 未识别出消息类型
                    break;
                case ReceiveXmlMessageType.Text:                               // 文本消息
                    break;
                case ReceiveXmlMessageType.Image:                              // 图片消息
                    break;
                case ReceiveXmlMessageType.Voice:                              // 语音消息
                    break;
                case ReceiveXmlMessageType.Video:                              // 视频消息
                    break;
                case ReceiveXmlMessageType.Location:                           // 地理位置消息
                    break;
                case ReceiveXmlMessageType.Link:                               // 链接消息
                    break;
                case ReceiveXmlMessageType.Event_QRCode_Subscribe:             // 用户未关注时扫描二维码事件
                    break;
                case ReceiveXmlMessageType.Event_QRCode_Scan:                  // 用户已关注时扫描二维码事件
                    break;
                case ReceiveXmlMessageType.Event_View:                         // 点击菜单跳转链接时事件
                    break;
                case ReceiveXmlMessageType.Event_Click:                        // 点击菜单拉取消息时事件
                    break;
                case ReceiveXmlMessageType.Event_Location:                     // 上报地理位置时事件
                    break;
                case ReceiveXmlMessageType.Event_Subscribe:                    // 关注事件
                    break;
                case ReceiveXmlMessageType.Event_UnSubscribe:                  // 取消关注事件
                    break;
                default:
                    break;
            }
        }
        return result;
    }
}</code></pre>

2、注册实现的接口

<pre><code class="language-csharp">WeiXinService.Register(_Service, appid, appsecret);</code></pre>

3、处理微信服务器发来的 xml

<pre><code class="language-csharp">WeiXinService.ProcessMessage(xml);</code></pre>
