> 欢迎访问我的博客[主页](https://nanalinshero.github.io)
## 从零开始搭建个人博客
我的个人博客的搭建修改自[Hux](http://huxpro.github.io)，以Hux的博客为模版，快速配置个人的GitHub Pages静态站点，并且可以通过git进行版本管理。
## Github Pages的优势
* 搭建简单而且免费；
* 支持静态脚本；
* 可以绑定你的域名——购买域名要花钱钱，还是白嫖香(⌒o⌒)；
* DIY自由发挥，动手实践一些有意思的东西：git,markdown,bootstrap,jekyll等；
* 理想写博环境：git+github+markdown+jekyll；
## 搭建和配置的主要流程
1. 开始：首先当然是注册git，然后选择你喜欢的博客模板，fork一下
2. 基础配置
3. 环境安装
4. 进阶配置：DIY来自定义你喜欢的配置
## 开始
git fork  
稍后更新
## 环境
[jekyll](http://jekyllcn.com/)安装与配置  
[mac系统👇](https://nanalinshero.github.io/2020/10/27/mac-install-jekyll/)
## 运行
运行并监听本地改变
``` 
jekyll server --watch 
```
运行预览草稿
``` 
jekyll server --drafts 
```
## 基础配置
图片、个人信息等的配置  
稍后更新
## 进阶配置
1. 侧边栏导航
2. 修改样式  
3. grunt  
通过Gruntfile.js来配置打包信息，常用的指令如下：  
```
grunt less #less预编译
grunt uglify #js编译

```
稍后更新