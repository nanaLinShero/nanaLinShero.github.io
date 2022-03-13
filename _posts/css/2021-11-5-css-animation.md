---
title: "CSS动画"
subtitle: "如何当一个合格的骗子"
layout: post
author: "Lin.na"
header-style: text
categories: css3
catalog:    true
tags:
  - CSS
  - 动画
---

> 有人说CSS3D是一个骗子.....

CSS用得不好，被揭穿，大家都直呼骗子；运用得当，那就是魔术师，接下来用4个例子来见证奇迹的时刻～
# 1.折叠展开
常见的超长文本折叠展开，都是用v-if/v-show来控制显示隐藏的，这里大家可以思考一下，不用js，如何用纯CSS实现常见的折叠展开？  
实现目标：
1. 模拟点击：点“*详情*”按钮展开，点“*收起*”按钮折叠
2. 多行文本显示按钮，单行文本不显示

![效果图](/img/css-animation/1-1.jpeg)

**揭秘**  
> 利用锚点定位：锚点做标记，快速定位

![效果图](/img/css-animation/1-2.png)
![效果图](/img/css-animation/1-3.png)

# 2.轮播
轮播图，相信大家都见得很多了，如何不用js，就实现图片轮播呢？  
3张图片轮播，最少需要用到多少个DOM元素？  
**揭秘**  
> 关键帧动画
>> 这里主要运用到了背景图background，利用关键帧动画，不断改变背景图的位置，实现轮播效果

![效果图](/img/css-animation/2-1.png)

# 3.旋转木马
游乐园的旋转木马，大家应该都见过，那如何让我们的图片也坐上旋转木马呢？  
![效果图](/img/css-animation/3-1.gif)

**揭秘**  
## 空间坐标轴  
![效果图](/img/css-animation/3-2.png)

3D transform的方法
```
rotateX( angle )

rotateY( angle )

rotateZ( angle )
```
何为rotate？
* 体操单杠运动是rotateX  
![效果图](/img/css-animation/3-3.gif)
* 小姐姐的钢管舞是rotateY  
![效果图](/img/css-animation/3-4.gif)
* 旋转飞刀的特技表演是rotateZ  
![效果图](/img/css-animation/3-5.gif)

> 旋转木马的旋转是沿着哪根轴运动的呢？答案：z轴。  
> 旋转木马图片的排布，是沿着哪根轴呢？答案：Y轴。

## perspective视角、透视
记得有篇课文，作者的老师让描画杨桃，其他人都是画出来是立体棱型的，唯独作者画出来是五角星型，为什么呢？就是因为作者坐的位置，视野不同，所以观察到的同一个事物形状不同。  
perspective就是人为的改变视角，让我们看到不一样的事物  
![效果图](/img/css-animation/3-6.png)

![效果图](/img/css-animation/3-7.png)

# 4.爱的魔力转圈圈
**揭秘**  
## 星空
画星星
```
box-shadow
```
流星的运动轨迹是哪根轴呢？答案：Z轴
流星
```
rotate
```
![效果图](/img/css-animation/4-1.png)
## 太极八卦图
![效果图](/img/css-animation/4-2.png)
线性渐变
```
linear-gradient
```
![效果图](/img/css-animation/4-3.png)
## 画圆
![效果图](/img/css-animation/4-4.png)

三角函数

![效果图](/img/css-animation/4-5.png)  
运用三角函数，计算出每个点的x坐标和y坐标，加上圆心的角度，就能绘制出圆形了
## 等边六边形
![效果图](/img/css-animation/4-6.png)  
多边形  
多边形的角度和
```
angle = （n-2）* 180
```
![效果图](/img/css-animation/4-7.png)  
![效果图](/img/css-animation/4-8.png)  
## 几何圆环
![效果图](/img/css-animation/4-9.png)  
径向渐变  
![效果图](/img/css-animation/4-10.png)  
![效果图](/img/css-animation/4-11.png)  
前面提到了线形渐变，这里绘制几何圆环运用到了径向渐变

# 总结
想要写好CSS动画，需要：
1. 熟悉CSS基本属性，
2. 掌握运动的本质，
3. 最后再加上亿点点数学知识

# 参考文档
1. 张鑫旭：[CSS3 3D transform变换](https://www.cnblogs.com/yangyang63963/p/5859913.html?utm_source=itdadao&utm_medium=referral)