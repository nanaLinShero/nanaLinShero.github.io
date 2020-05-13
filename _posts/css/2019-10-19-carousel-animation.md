---
title: "css3关键帧动画实现轮播效果"
subtitle: "保姆级教程，手把手教会使用"
layout: post
author: "Lin.na"
header-style: text
catalog:    true
tags:
  - CSS
---

> 本文首发于我的博客园博客 [css3关键帧动画实现轮播效果](https://www.cnblogs.com/CodeShero/p/7265855.html)，转载请保留链接 ;)

## 实现效果
打开手机京东，可以看到首页的头部，以这个头部为基础，仿写一个类似的样式。

## 思路
仔细观察可以发现，手机京东的头部是以一个搜索栏和轮播特效组成的，而这个搜索栏是以轮播特效做为背景的，现在运用css3关键帧动画，可以实现这样的头部效果。

## 测试
首先，写一个简单的测试来验证思路是否正确，这样可以排除其他样式的干扰；测试如下：

1. 两个嵌套的div，内部div1以简单的文字和图片模拟的搜索栏

```html
<body>
    <div class="diva">
        <div class="div1">头部
            <img src="../img/放大镜.png">
        </div>
    </div>
</body>
```

2. 由于动画的主要原理在于改变背景图片的位置，这里先介绍一下background-img，知道的同学自行跳过吧
* 由url插入图片

```css
div{
    width: 300px;
    height: 200px;
    background: red;
    background-image: url(../img/放大镜.png);
}
```

效果：
![效果图](/img/in-post/post-carousel/carousel-1.jpg)
* 很明显看到，背景图片的大小不适合div的宽高，所以，用background-size设置图片的宽高

```css
background-image: url(../img/放大镜.png);
background-size: 20px 30px;
```

效果：
![效果图](/img/in-post/post-carousel/carousel-2.jpg)
* 因为背景图默认的设置是重复背景图片，所以更改为禁止重复

```css
background-image: url(../img/放大镜.png);
background-size: 20px 30px;
background-repeat: no-repeat;        /*禁止图片重复*/
```

效果：
![效果图](/img/in-post/post-carousel/carousel-3.jpg)
* 这个时候呢，假如想调整图片的位置，就需要设置图片的position

```css
background-image: url(../img/放大镜.png);
background-size: 20px 30px;
background-repeat: no-repeat;        /*禁止图片重复*/
background-position: 100px 50px;        /*这里设置的是px坐标，也可以用left或者百分比的形式设置图片位置*/
```

效果：
![效果图](/img/in-post/post-carousel/carousel-4.jpg)
3. 给外部diva设置宽度、背景色和边框，便于观察；给内部div1添加宽高和背景图片，注意这里div1的宽度是背景图片宽度的总和；当然，div1中的图片也要适当调整宽高。

```css
.diva{
    width: 100%;
    background: red;
    border: 5px solid blue;
}
.div1{
    width: 900px;
    height: 200px; 
    background-image: url(../img/轮播1.jpg),url(../img/轮播2.jpg),url(../img/轮播3.jpg);
    background-repeat: no-repeat;
    background-size: 300px 200px;
    background-position: 0 0,300px 0,600px,0;
}
.div1 img{
    width: 20px;
    height: 20px;
}
```

大概就是这个效果啦
![效果图](/img/in-post/post-carousel/carousel-5.jpg)
4. 将div1的宽度设置为一张图片的宽度，就定义一个相当于用户的可见窗口

```css
.div1{
    width: 300px;        /*设置div宽度为一张图片的宽度*/
    height: 200px; 
    border: 10px solid green;
    background-image: url(../img/轮播1.jpg),url(../img/轮播2.jpg),url(../img/轮播3.jpg);
    background-repeat: no-repeat;
    background-size: 300px 200px;
    background-position: 0 0,300px 0,600px,0;
}
```

效果：
![效果图](/img/in-post/post-carousel/carousel-6.jpg)
5. 由于设置的窗口大小，剩余的两张图片不可见了，相当于屋子里面有三个人，你从一个窗口看进去，只看到了一个人，其他人被墙壁遮住了，这时如果这个人往左走，离开窗口，第二个人走到窗口位置，就可以看到第二个人了。

```css
.div1{
    width: 300px;        /*设置div宽度为一张图片的宽度*/
    height: 200px; 
    border: 10px solid green;
    background-image: url(../img/轮播1.jpg),url(../img/轮播2.jpg),url(../img/轮播3.jpg);
    background-repeat: no-repeat;
    background-size: 300px 200px;
    /*background-position: 0 0,300px 0,600px,0;*/
    background-position: -300px 0,0 0,300px,0;        /*图片左移*/
}
```

效果：
![效果图](/img/in-post/post-carousel/carousel-7.jpg)
6. 当这三个人不断重复这种移动，就会对窗户外的你形成轮播效果，css3的关键帧动画就可以实现这种重复不断的移动，不了解的同学可以自行百度，这里就不细说关键帧动画原理了。

**css3关键代码：**

```css
.home{
    width: 320px;        /*为了适应iphone5的分辨率设置的宽度*/
    height: 200px;
    background: url(../img/轮播1.jpg),url(../img/轮播2.jpg),url(../img/轮播3.jpg),url(../img/轮播1.jpg);
    /*第四张图片与第一张图片一致是为了轮播的时候效果更加自然，否则从最后一张播放到第一张会造成生硬的停顿*/
    
    background-repeat: no-repeat;
    background-size: 320px 200px;
    animation: kbg 9s linear infinite;
    /*调用kbg关键帧动画,动画时长为9s，匀速运动，无限循环播放(除非页面被关闭)*/
}
@keyframes kbg{
    0%{
        background-position: 0 0,320px 0,640px 0,960px 0;
    }
    5%{
        background-position: 0 0,320px 0,640px 0,960px 0;
    }

    30%{
        background-position: -320px 0,0 0,320px 0,640px 0;
    }
    40%{
        background-position: -320px 0,0 0,320px 0,640px 0;
    }

    60%{
        background-position: -640px 0,-320px 0,0 0,320px 0;
    }
    70%{
        background-position: -640px 0,-320px 0,0 0,320px 0;
    }

    95%{
        background-position: -960px 0,-640px 0,-320px 0,0 0;
    }
    100%{
        background-position: -960px 0,-640px 0,-320px 0,0 0;
    }
}
```

## 总结
关键帧轮播的视觉效果就和手机京东差不多，所缺的就是一些细节的地方。可能有人说网上的轮播器一大把,这样做是重复造轮子，但是我坚信学以致用，多练习才能理解和掌握知识要点。
## 题外话
小妹初来乍到，望大家捧个人场，多多评论指正，最好加个关注呢，期待和各位的交流~