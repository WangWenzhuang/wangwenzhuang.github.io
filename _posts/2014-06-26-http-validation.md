---
layout: post
title: "HTTP GET 方法的简单访问效验"
description: "自定义一套签名算法，接口和请求者使用签名算法一致，并使用一致的 token。请求接口时将签名结果作为必要参数，接口收到请求效验签名合法性。"
category: 技术
tags: ["HTTP GET 效验"]
published: true
---

## 情景

有这样一个获取数据的接口，此接口需要效验合法性，如果效验通过则返回正确数据。

## 解决方案

自定义一套签名算法，接口效验和请求者使用签名算法一致，并使用一致的 token。请求接口时将签名结果作为必要参数，接口收到请求效验合法性。

## 代码

### 公用的生成签名类

<pre><code class="language-csharp">public sealed class SignatureHelper
{
    /*
     * 必备参数：token、时间戳、随机数（9位）
     * 生成规则：对参数进行排序生成sha1哈希（不带符号）
     *
     * 2014/5/4
     *
     * 王文壮
     */
    /// <summary>
    /// 生成签名
    /// </summary>
    public static string CreateSignature(Array array)
    {
        Array.Sort(array);
        string tmpStr = string.Empty;
        foreach (var tmp in array)
        {
            tmpStr += tmp;
        }
        return BitConverter.ToString(
            new SHA1CryptoServiceProvider().ComputeHash(
                new ASCIIEncoding().GetBytes(tmpStr)
            )
        ).Replace("-", string.Empty).ToLower();
    }

    /// <summary>
    /// 生成时间戳
    /// 规则：1970年1月1日至今的间隔秒数
    /// </summary>
    public static string CreateTimestamp()
    {
        return ((int)DateTime.Now.Subtract(
            new DateTime(1970, 1, 1)).TotalSeconds
        ).ToString();
    }

    /// <summary>
    /// 创建9位随机数
    /// </summary>
    public static string CreateRandomNumber()
    {
        return new Random().Next(100000000, 999999999).ToString();
    }

    /// <summary>
    /// 效验签名
    /// </summary>
    public static bool CheckSignature(
        string token,
        string signature,
        string timestamp,
        string nonce)
    {
        string[] tempArr = { token, timestamp, nonce };
        var tmpStr = SignatureHelper.CreateSignature(tempArr);
        return tmpStr.Equals(signature);
    }
}</code></pre>

接口定义

<pre><code class="language-csharp">/*
 * signature：签名结果
 * timestamp：时间戳
 * nonce：随机字符串
 */
[HttpGet]
public string GetData(string signature, string timestamp, string nonce)
{
    var result = string.Empty;
    var token = "wangwenzhuang";
    if (!string.IsNullOrEmpty(signature)
        && !string.IsNullOrEmpty(timestamp)
        && !string.IsNullOrEmpty(nonce))
    {
        // 可以检测时间是否超时
        if (CheckTimeOut(timestamp))
        {
            // 检测签名的合法性
            if (SignatureHelper.CheckSignature(
                token,
                signature,
                timestamp, nonce))
            {
                result = "我是测试数据";
            }
        }
    }
    return result;
}

private bool CheckTimeOut(string timestamp)
{
    var result = default(bool);
    var now = int.Parse(SignatureHelper.CreateTimestamp());
    int time;
    if (int.TryParse(timestamp, out time))
    {
        // 超过30秒网页就过期
        if (now - time >= 30)
        {
            result = false;
            LogHelper.Log("网页过期");
        }
        else
        {
            result = true;
        }
    }
    else
    {
        result = false;
    }
    return result;
}</code></pre>

请求

<pre><code class="language-csharp">public static string TestGetData()
{
    var timestamp = SignatureHelper.CreateTimestamp();
    var nonce = SignatureHelper.CreateRandomNumber();
    var signature = SignatureHelper.CreateSignature(
        new string[] { "wangwenzhuang", timestamp, nonce });
    var url = string.Format(
        "/GetData?signature={0}&timestamp={1}&nonce={2}",
        signature,
        timestamp,
        nonce);
    // 请求代码...
}</code></pre>