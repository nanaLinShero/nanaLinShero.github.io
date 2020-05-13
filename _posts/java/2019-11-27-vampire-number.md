---
title: "三重循环实现四位的吸血鬼数"
subtitle: "对三重循环的理解与掌握"
layout: post
author: "Lin.na"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
tags:
  - Java
---

> 本文首发于我的博客园博客 [三重循环实现四位的吸血鬼数](https://www.cnblogs.com/CodeShero/p/7238815.html)，转载请保留链接 ;)

## 什么是吸血鬼数？
吸血鬼数字是指位数为偶数的数字，可以由一对数字相乘而得，而这对数字各包含乘积的一半位数的数字，其中从最初的数字中抽取的数字可以任意排序。以两个0结尾的数字是不允许的。  
例如下列的数字都是"吸血鬼"数字：

```
1260=21*60
1827=21*87
2187=27*81
```

## 实现思路
将四位数按位拆分为四个数字，由这四个数字组合成两个两位数，判断这两个数的乘积是否等于原四位数。
## 数学的组合逻辑
1. 两个数字之间是无序的，即21\*60和60\*21是等价的  
2. 十位和个位的数字是有序的，即12和21是不同的  

## 如何循环？
* 外循环：固定一个数字作为十位数，其余三个数字循环作为个位数  
* 内循环：以剩下的三个数循环，排除已被选中的数，再计算出两个数的乘积；将第一个数的个位和十位转换位置再计算判断  

## 伪代码---提供思路

```java
for(i从1000循环到9999取四位数){
　　取这个四位数的个、十、百、千位上的数字存放到数组a；
　　if(个位和十位的数字都为0){
　　　　停止执行当前迭代，退回到循环起始处，开始下一次循环；
　　}
　　for(j从1到3循环){
　　　　for(k从1到3循环){
　　　　　　if(k不等于j){
　　　　　　　　从数组中取出相应的两位数字，计算乘积；
　　　　　　　　if(乘积等于四位数i){
　　　　　　　　　　打印吸血鬼数；
　　　　　　　　}
　　　　　　　　将这个两位数的个位和十位转换位置，计算乘积；
　　　　　　　　if(乘积等于四位数i){
　　　　　　　　　　打印吸血鬼数；
　　　　　　　　}
　　　　　　}
　　　　}
　　}
}
```

## java代码：

```java
package operator;
public class VimpireFigures {
　　public static void main(String[] args) {
　　　　System.out.println("四位数的吸血鬼数：");
　　　　int p1,p2,p;
　　　　int a[]=new int[4];
　　　　inner: 　　	//跳转标签
　　　　for(int i=1000;i<10000;i++){
　　　　　　a[0]=i%10;
　　　　　　a[1]=i/10%10;
　　　　　　a[2]=i/100%10;
　　　　　　a[3]=i/1000%10;
　　　　　　if(a[1]==0&&a[0]==0){
　　　　　　　　continue;
　　　　　　}
　　　　　　for(int j=1;j<4;j++){
　　　　　　　　for(int k=1;k<4;k++){
　　　　　　　　　　if(k!=j){
　　　　　　　　　　　　p1=a[0]*10+a[j];　　//以a[0]为固定数字
　　　　　　　　　　　　p2=a[k]*10+a[6-k-j-0];
　　　　　　　　　　　　p=p1*p2;
　　　　　　　　　　　　if(p==i){
　　　　　　　　　　　　　　System.out.print(a[3]+" "+a[2]+" "+a[1]+" "+a[0]+" ");
　　　　　　　　　　　　　　System.out.print(p1+"*"+p2+"=");
　　　　　　　　　　　　　　System.out.println(i);
　　　　　　　　　　　　}
　　　　　　　　　　　　p1=a[j]*10+a[0];　　//个位和十位交换位置
　　　　　　　　　　　　p=p1*p2;
　　　　　　　　　　　　if(p==i){
　　　　　　　　　　　　　　System.out.print(a[3]+" "+a[2]+" "+a[1]+" "+a[0]+" ");
　　　　　　　　　　　　　　System.out.print(p1+"*"+p2+"=");
　　　　　　　　　　　　　　System.out.println(i);
　　　　　　　　　　　　　　if(a[k]==a[j]){
　　　　　　　　　　　　　　　　break inner; 　　//当k和j相等时，会出现重复，所以一次计算后就跳转到标签位置
　　　　　　　　　　　　　　}
　　　　　　　　　　　　}
　　　　　　　　　　}
　　　　　　　　}
　　　　　　}
　　　　}
　　}
}
```

## 运行结果：
![运行结果](/img/in-post/java/vampire-result.jpg)