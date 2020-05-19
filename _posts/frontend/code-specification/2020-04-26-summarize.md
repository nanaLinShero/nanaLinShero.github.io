---
title: "前端代码规范"
subtitle: "TSA与BFC整合后要遵守的代码约定"
layout: post
author: "Lin.na"
header-style: text
tags:
  - 前端
---

## 概述
### 关于
前端代码规范是基于W3C等官方文档，并结合团队日常业务需求以及团队在日常开发过程中总结提炼出的经验而制定。  
旨在增强团队开发协作、提高代码质量和打造开发基石的编码规范。  
### TSA前端代码现状
TSA前端代码，引用深蓝平台1.3.5版本，采用的框架是Angularjs，UI采用semantic(semantic基于Jquery)+深蓝平台(深蓝平台是对semantic的二次封装和通用组件的封装)，js工具库采用lodash，接口请求模拟采用mockjs，样式采用的stylus，打包工具webpack

```
框架：Angularjs
UI：深蓝平台+Semantic
js库：lodash
请求模拟：mockjs
Style：stylus
打包工具：webpack
```
### TSA前端框架和UI改进
TSA框架由Angularjs转为React，引入了dev控件库作为新的UI框架，保留原有代码的基础上进行的更新，所以老代码的维护还是采用以前的形式，新功能的开发，均采用新框架和新UI。
### 特殊符号含义
本文档与bfc的前端规范文档进行整合，特殊的规范将以如下符号标识：
```
-bfc：bfc规范文档提出的规范
-tsap：bfc和tsa的规范文档所共有的规范
!：重点规范，不遵守可能造成代码错误的规范
```
以下规范在持续更新中：
* 命名规范
* HTML规范
* CSS规范
* JavaScript规范