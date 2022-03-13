---
title: "认识跨域"
subtitle: "对跨域的初步了解"
layout: post
author: "Lin.na"
header-style: text
categories: web
tags:
  - 浏览器
  - 跨域
---

# 0.写在最前面

在与后端的联调中，由于后端接口部署到rd环境，但前端开发在test环境，此时请求接口，显然是一个跨域请求，但此时浏览器并未报错跨域，而是将原本的post请求转换为options请求，如下图：  
![response](/img/cross-domain/1.png)

首先经过问题排查，锁定是跨域造成的，那么，到底什么是跨域？跨域又该如何处理呢？

# 1.什么是跨域？
浏览器的同源策略：限制了当前源对另一个源的资源进行交互。  
即不在同一个源下的请求，就会造成跨域。  
同源：两个URL的协议(protocol)、端口(port)和主机(host)三者都相同，则这两个URL是同源的。  
协议主要是http协议和https协议的区别。

> 以当前联调为例，前端项目在test.com，而后端接口部署在rd.com，test.com和rd.com的主机不一致，不属于同源，从test发起对rd的请求，就会造成跨域。

同源策略的限制范围：
* Cookie、localStorage、IndexDB⽆法读取。
* DOM⽆法取得。
* AJAX请求不能发送。

> 这个AJAX请求已经发出去了，服务端也接收到并处理了，但是返回的响应结果不是浏览器想要的结果，所以浏览器将这个响应的结果给拦截了，这就是为什么上图的response返回的结果是failed。

三个允许跨域加载的标签  
``` html
<img src=XXX>
<link href=XXX>
<script src=XXX>
```
# 2.如何实现跨域请求？
虽然同源策略出于安全考虑，但在实际开发时，跨域请求是必要的，特别是在微前端的架构当中。  
实现跨域的方案有：
  - CORS
  - JSONP
  - Web sockets
  - postMessage
  - window.name + iframe
  - location.hash + iframe
  - 动态创建srcipt
  - document.domain + iframe(主域相同才能使用)
  - nginx反向代理服务器

由于CORS比较陌生，且此次联调主要涉及CORS跨域处理，以下重点介绍CORS。
## 2.1.跨域资源共享CORS
CORS：一个W3C标准，它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服AJAX只能同源使用的限制。  
CORS需要**浏览器**和**服务器**同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。  
实现CORS通信的关键是**服务器**。只要服务器实现了CORS接口，就可以跨源通信。  
浏览器将CORS请求分成两类：简单请求和非简单请求。  
只要同时满足以下两大条件，就属于简单请求。  
1. 请求方法是以下三种方法之一：
```
HEAD
GET
POST
```
2. HTTP的头信息不超出以下几种字段：
```
Accept
Accept-Language
Content-Language
Last-Event-ID
Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain
```
不满足这两个条件的，就是非简单请求。  
## 2.2.简单请求
配置简单请求头header，一般是配置Content-Type，其他什么也不用做，就是正常发请求就可以。  
如果简单请求还会报错，就看响应响应信息中是否有Access-Control的三个字段，如果没有，表明是后端没有配置跨域，如下图：  
![error](/img/cross-domain/2.png)
![response headers](/img/cross-domain/3.png)
## 2.3.非简单请求
当发起跨域请求时，浏览器会自动触发预检请求，预检请求用的请求方法是OPTIONS，表示这个请求是用来询问的。预检请求得到服务端的响应，该响应回复是否支持跨域，如果支持跨域，则浏览器发起正常请求，如果不支持，则返回请求错误信息，控制台报错。整个请求流程如下图：
![请求流程图](/img/cross-domain/4.png)
由此可见，非简单请求的一次发起，会触发两个请求，比较消耗性能。  
当服务器对请求做响应时，公司在**网关**对非简单请求进行处理和过滤，禁止所有预检请求，即options请求。整个响应处理流程如下图：
![请求流程图](/img/cross-domain/5.png)
# 3.总结
简单来说，经常使用的跨域解决方案CORS，就是需要后端在服务器进行配置，平时前端开发人员并不关心如何实现，也基本感知不到跨域请求的差异，所以一旦服务器配置不当，跨域的问题就暴露出来了。后端同学如果是通过postman发起请求测试接口成功，那么关于跨域问题的定责，就需要前端对跨域相关知识有一定的了解，才能第一时间反馈问题到后端处理。
# 参考文档
1. MDN Web Docs：[浏览器的同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy) 
2. 阮一峰：[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
3. 多点研发： [跨域问题](https://duodian.feishu.cn/docs/doccnlThh5RdHPgaYfk6k4s3C4g?new_source=message#EFmIqb)
4. segmentfault：[不要再问我跨域问题了](https://segmentfault.com/a/1190000015597029)