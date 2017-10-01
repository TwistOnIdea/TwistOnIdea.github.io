---
layout:     post
title:      "关于@font-face将图标嵌入到网页"
subtitle:   "Insert the icons into the webpage"
date:       2017-10-1 12:00:00
author:     "Twist"
header-img: "img\in-post\post-css-fontface/header-img.jpg"
catalog:    true
tags:
    - CSS
    - @font-face
    - IcoMoon
---



>由@**font-face**引发的一系列有趣的探索，源于搭建博客时对[Portfolio](https://twistonidea.github.io/portfolio/)分类下的卡片块下的标识icon的兴趣。  


![1](/img/in-post/post-css-fontface/icon.png)

##  何为@font-face？

* @font-face 不能说他是什么新东西了，在 CSS2.0 规范中就有了这玩意儿，IE4.0 开始就已经出现，只是当时用的不是特别广泛，后来在 CSS2.1 草案中又被删掉。随着 web 的急速发展，@font-face 价值越来越凸显，然后再次被纳入 CSS3 草案中

* 官方点来说的话，它是一个CSS规则，允许你把自己定义的Web字体嵌入到网页当中。在CSS3之前，web设计师必须使用已在计算机上安装好的字体。

* 而通过CSS3，web设计师再也不必被迫使用"web-safe"字体了，他们可以使用任意他们喜欢的字体，将字体文件存放到web服务器上，它会在需要时被自动下载到用户的计算机上。

**@font-face的语法规则：**
```css
   @font-face {
      font-family: <YourWebFontName>;
      src: <source> [<format>][,<source> [<format>]]*;
      [font-weight: <weight>];
      [font-style: <style>];
    }
```


>这无疑是给那些前端设计们打开了一个全新的世界

##  Tff、Eot、Otf、Woff、Svg？

现在已经大致了解了@font-face的概况和好处，但在应用方面不仅需要了解上述，还需要考虑字体类型对于浏览器的兼容性，所以先简单介绍下字体类型的几大分类：

* **TrueType（.tff）**
.ttf字体是Windows和Mac的最常见的字体，是一种RAW格式，因此他不为网站优化,支持这种字体的浏览器有【IE9+,Firefox3.5+,Chrome4+,Safari3+,Opera10+,iOS Mobile Safari4.2+】

* **EOT– Embedded Open Type (.eot)**
.eot字体是IE专用字体，可以从TrueType创建此格式字体,支持这种字体的浏览器有
【IE4+】

* **OpenType(.otf)**
.otf字体被认为是一种原始的字体格式，其内置在TureType的基础上，所以也提供了更多的功能,支持这种字体的浏览器有【Firefox3.5+,Chrome4.0+,Safari3.1+,Opera10.0+,iOS Mobile Safari4.2+】

* **WOFF–WebOpen Font Format (.woff)**
.woff字体是Web字体中最佳格式，他是一个开放的TrueType/OpenType的压缩版本，同时也支持元数据包的分离,支持这种字体的浏览器有【IE9+,Firefox3.5+,Chrome6+,Safari3.6+,Opera11.1+】

* **SVG(Scalable Vector Graphics) Fonts (.svg)**
.svg字体是基于SVG字体渲染的一种格式,支持这种字体的浏览器有【Chrome4+,Safari3.1+,Opera10.0+,iOS Mobile Safari3.2+】。


所以这就意味着在@font-face中我们需要多种格式的字体来达到更多浏览器版本的支持。

为了使@font-face达到更多的浏览器支持，[Paul Irish](http://paulirish.com/)写了一个独特的@font-face语法叫[Bulletproof @font-face](http://paulirish.com/2009/bulletproof-font-face-implementation-syntax/)


```css
   @font-face {
	font-family: 'YourWebFontName';
	src: url('YourWebFontName.eot?') format('eot');/*IE*/
	src:url('YourWebFontName.woff') format('woff'),
	url('YourWebFontName.ttf')format('truetype');/*non-IE*/
   }
```
为了让更多浏览器支持，可以写成

```css
 @font-face {
	font-family: 'YourWebFontName';
	src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
	src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
             url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
             url('YourWebFontName.ttf')  format('truetype'), /* Safari, Android, iOS */
             url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */
   }
```
说那么多规则以及字体类型方面的定义，并没有发现什么有趣的事情，反倒会更加加深对这些理论的枯燥理解，其实非然。

##  图标 = 字体？！

###  IcoMoon？？？

![2](/img/in-post/post-css-fontface/2.png)


```
IcoMoon is an icon solution, providing three main services: Vector Icon Packs, The IcoMoon App, and hosting icons as SVGs or fonts. Read further to learn about each service in detail.
```
什么是[IcoMoon](https://icomoon.io/#docs/intro)？官方文献给出了简短的回答。这个网站，准确说是个应用，**提供矢量图标包使用，以及图标的应用处理，最后可以将你的图标打包，导出SVGs和Fonts格式。**

免费提供的[图标包](https://icomoon.io/app/#/select/library)质量挺高，区域涵盖生活，办公，Brand Logo等方面需求，当然也有更多购买的需求包，可以自行查看。

###  IcoMoon App

接下来进入有趣之处，它对网站的[应用处理](https://icomoon.io/app/#/select)。

将页面分为上中下三个板块...

![5](/img/in-post/post-css-fontface/5.png)

####  左上角的下拉菜单（入口）

对*本地图标项目的进行导入、创建*，也可以通过从Icon library中导入或选中图标的方法来创建个人的项目。

除此之外还有个人的登录以及查看官方的使用说明操作。

####  上方工具栏
对图标进行简单的*选择、编辑、删除、移动、搜索等处理*。

Import Icons按钮只能*choose SVG images, SVG fonts or JSONs exported by IcoMoon*，导入之前需要对格式注意。

形似铅笔状的edit的功能比较丰富，可以对图标进行一些自定义的操作，*顺/逆旋转，放大/小，左/右移动，承载图标区域的宽度增/减，图标位于区域上/下/左/右/中部的调整等*。Tags，Names可以在后续步骤中，做全局调整。

![6](/img/in-post/post-css-fontface/6.png)

####  中部项目图标视图

通过每个项目栏目左上角的下拉菜单按钮，对项目下的大量图标进行整理，挑选，比较人性化的操作的是
> Duplicate Selectiion： Here将选中的图标以复制的形式移到所有图标的头部

> Move Selection Here：将选中的图标移到所有图标的头部
以便对选完的图标有个条理的概览。

并且可以对自己挑选或设计的一套图标加上自己的Metadata，即下图所示

![metadata](/img/in-post/post-css-fontface/metadata.png)

最后，也是最重要的一点**Download JSON**,将此项目信息保存下来，防止浏览器缓存清除后，项目丢失。将JSON保存，如果有后续的修改或添加可以通过Import Icons将项目导入进行再次的编辑。

###  Generate Font
选完自己需要的图标后，然后选择下方功能栏进入**Generate Font**页面。

页面也是分上中下三个板块...

####  Reset char codes or ligatures

![codes-liga](/img/in-post/post-css-fontface/codes-liga.gif)

页面上部的功能栏，可以选择对图标的*Codes*和*Ligatures*的显示，查看页面中部的图标的属性
![edit](/img/in-post/post-css-fontface/edit.png)

可以通过**Reset**按钮对*Codes*和*Ligatures*的全局设置，将Codes从e001开始设置，方便引用

再通过get code来查看CSS中如何引用这个符号（）

![get-code](/img/in-post/post-css-fontface/get-code.png)

#### Preferences

Preferences主要*对项目进行正式的封装*，简单用一张图介绍

![preference](/img/in-post/post-css-fontface/preference.png)

关于图标基线的设置，官方说明是这样的

![baseline](/img/in-post/post-css-fontface/baseline.png)

> 百分比数值越大，基线越高...

####  Qucik Usage and Sharing

![quick-usage](/img/in-post/post-css-fontface/quick-usage.png)

暂时提供一个link可供24小时内使用，如果需求永久link可以购买高级的权限...

###  Download

####  Fonts Download

![fonts-download](/img/in-post/post-css-fontface/fonts-download.png)

####  Svg Download

![svg-download](/img/in-post/post-css-fontface/svg-download.png)

对下载下来的文件，这里不一一赘述了...

##  应用
在html中添加行内元素

```
<span class="cbp_tmicon-Name"></span>

```
并在CSS中加入已下载文件中的style.css

即可实现如开头所示的效果了...


