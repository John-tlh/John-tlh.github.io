---
title: 关于CORS
category: 
- 渗透测试
---

## CORS 知识梳理

### 简介

CORS是为了解决浏览器的同源策略限制。浏览器一旦发现当前源发送了一个跨源请求（xmlhttprequest或者ajax）就会自动添加一些附加的头信息一起发送给服务器。

因此只要服务器实现了cors的配置，就可以跨源通信。

### 简单请求和非简单请求

- 简单请求（simple request）

请求方式为get、head、post并且http头信息不超出五个特定字段。

- 非简单请求（not-so-simple request）

### 跨域基本流程

**step1：**

对于简单请求，浏览器会在请求头之中加一个Origin字段。比如：

```http
GET /cors HTTP/1.1
Origin: http://api.bob.com:8000
Host: api.alice.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0
```

`Origin`字段用来说明，本次请求来自哪个源。

**step2：**

服务器收到这个请求会进行判断，如果这个字段值指定的源不在许可范围内会返回一个正常的响应也就是不包含access-control-origin字段。并且抛出一个错误给xmlhttprequest的回调函数。如果指定的源在许可范围内，服务器返回的响应会多出几个字段：

```http
Access-Control-Allow-Origin: http://api.bob.com:8000
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: FooBar
Content-Type: text/html; charset=utf-8
```

**（1）Access-Control-Allow-Origin**

该字段是必须的。它的值要么是请求时`Origin`字段的值，要么是一个`*`，表示接受任意域名的请求。

**（2）Access-Control-Allow-Credentials**

该字段可选。它的值是一个布尔值，表示是否允许发送Cookie。默认情况下，Cookie不包括在CORS请求之中。设为`true`，即表示服务器明确许可，Cookie可以包含在请求中，一起发给服务器。这个值也只能设为`true`，如果服务器不要浏览器发送Cookie，删除该字段即可。

**（3）Access-Control-Expose-Headers**

该字段可选。CORS请求时，`XMLHttpRequest`对象的`getResponseHeader()`方法只能拿到6个基本字段：`Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`、`Pragma`。如果想拿到其他字段，就必须在`Access-Control-Expose-Headers`里面指定。上面的例子指定，`getResponseHeader('FooBar')`可以返回`FooBar`字段的值。

<!-- more -->