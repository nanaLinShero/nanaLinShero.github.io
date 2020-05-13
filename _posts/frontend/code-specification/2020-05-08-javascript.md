---
title: "JavaScript规范"
subtitle: "TSA与BFC整合后要遵守的代码约定"
layout: post
author: "Lin.na"
header-style: text
tags:
  - 前端
---

## JavaScript规范
JavaScript遵循最大限度的可复用，可读性强，便于维护的原则。
### 语言规范
#### 变量声明
const 和 let 都是块级作用域，var 是函数级作用域  
使用规范：
* 变量声明使用const和let，不使用var
* 常量声明，使用const
* 变量声明，使用let
#### 对象
* 使用对象方法的简写方式
``` javascript
// bad
const item = {
  value: 1,

  addValue: function (val) {
    return item.value + val
  }
}

// good
const item = {
  value: 1,

  addValue(val) {
    return item.value + val
  }
}
```
* 使用对象属性值的简写方式
``` javascript
const job = 'FrontEnd'

// bad
const item = {
  job: job
}

// good
const item = {
  job
}
```
* 对象属性值的简写方式要和声明式的方式分组
``` javascript
const job = 'FrontEnd'
const department = 'JDC'

// bad
const item = {
  sex: 'male',
  job,
  age: 25,
  department
}

// good
const item = {
  job,
  department,
  sex: 'male',
  age: 25
}
```
#### 数组
* 使用拓展运算符 ... 复制数组（注意：浅拷贝）
``` javascript
// bad
const items = []
const itemsCopy = []
const len = items.length
let i

// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i]
}

// good
itemsCopy = [...items]
```
#### 解构赋值
* 当需要使用对象的多个属性时，请使用解构赋值
``` javascript
// bad
function getFullName (user) {
  const firstName = user.firstName
  const lastName = user.lastName

  return `${firstName} ${lastName}`
}

// good
function getFullName (user) {
  const { firstName, lastName } = user

  return `${firstName} ${lastName}`
}

// better
function getFullName ({ firstName, lastName }) {
  return `${firstName} ${lastName}`
}
```
* 当需要使用数组的多个值时，请同样使用解构赋值
``` javascript
const arr = [1, 2, 3, 4]

// bad
const first = arr[0]
const second = arr[1]

// good
const [first, second] = arr
```
* 函数需要回传多个值时，请使用对象的解构，而不是数组的解构
``` javascript
// bad
function doSomething () {
  return [top, right, bottom, left]
}

// 如果是数组解构，那么在调用时就需要考虑数据的顺序
const [top, xx, xxx, left] = doSomething()

// good
function doSomething () {
  return { top, right, bottom, left }
}

// 此时不需要考虑数据的顺序
const { top, left } = doSomething()
```
#### 字符串
* 字符串统一使用单引号的形式 ''
``` javascript
// bad
const department = "TSA"

// good
const department = 'TSA'
```
* 字符串太长的时候，请不要使用字符串连接符换行 \，而是使用 +
``` javascript
const str = '全流量分析 全流量分析 全流量分析 ' +
  '全流量分析 全流量分析 全流量分析 ' +
  '全流量分析 全流量分析 全流量分析 '
```
* 程序化生成字符串时，请使用模板字符串
``` javascript
const test = 'test'

// bad
const str = ['a', 'b', test].join()

// bad
const str = 'a' + 'b' + test

// good
const str = `ab${test}`
```
