#问题
一个宽度960像素固定的居中页面。假如首页内容较短，是一个完整的页面，右侧没有滚动条，不需要下拉。点击其中一个日志后，日志比较长，新的页面在右侧就会出现一个滚动条。显示器分辨率的宽度是1024像素，新日志的可视页面因为右侧出现了滚动条而变小了。可能只有1020像素。那么整个居中的页面在点击的时候，就会向左略微移动一点。对于强迫症的人来说，感觉很不爽。

#方法
让网页略微大一点点，首页就有滚动条。但是在火狐浏览器无效。
```html
html {
    height: 100%;
    margin-bottom: 0.01em;
}
```

#方法
高度高一点点
```html
html {
    height: 102%;
}
```

#方法
```html
html {
	overflow-y: scroll; 
}
```
始终显示滚动条。兼容主流浏览器，最优解。



#概要
实现当前页面导航条高亮

#旧方法
每个页面的li要增加一个class，这样每个页面的导航的HTML是不一样的，破坏了代码的完整性。
```html
<ul>
  <li><a class="selected" href="#">Home</a></li>
  <li><a href="#">About us</a></li>
  <li><a href="#">Contact us</a></li>
</ul>
```

#解决方法
HTML页面保持原样
```html
<ul>
  <li><a class="home"  href="#">Home</a></li>
  <li><a class="about" href="#">About us</a></li>
  <li><a class="contact" href="#">Contact us</a></li>
</ul>
```
CSS增加以下代码
```css
#home .home, #about .about, #about .about, #contact .contact
{
Your CSS stylings here
}
```
给每个页面的body标签，增加ID选项。例如body id="home" 这样当前页面就会高亮。



#问题
- 搜索引擎很重视网页文字结构，而且标题h1在网页的权重很大。
- 如果不想使用文字作为标题，而想使用图片作为标题，搜索引擎无法查看到文字内容，就会对搜索引擎不友好。

#解决方法
同时使用文字和图片，使用CSS样式，把文字移出到屏幕外。
```css
.headerReplacement {
   text-indent: -9999px;
   width: 600px;
   height: 100px;
   background: url(pathtoyourimage) #cccccc no-repeat;  
}
```

#总结
- 使用图片标题替换了不美观的纯文字标题
- 对搜索引擎友好。
- 关闭CSS和使用屏幕阅读器的人，也可看到文字。



在分配ID和类名称时，一定要尽可能保持名称与表现方式无关。

div可是用来对块级元素进行分组，而span可以用来对行内元素进行分组或标识。

XHTM1.1是非常严格的模式，只要有错误，网页就不会显示。因此更推荐XHTML1.0

#子选择器
div>li,只选择元素的直接后代。

IE7中，父元素和子元素之间有注释，就会出问题。

在IE6或者更低的版本中，可以使用通用选择器模拟自选择器的效果。先用后代选择器选上应有的效果，再用通用选择器覆盖子元素的后代上的样式。
```css
#nav li{
padding:10px
}
#nav li *{
padding:10px
}
```

#特殊性
![](https://leanote.com/api/file/getImage?fileId=567e050aab6441660a007574)

添加一个父级元素的ID，提高特殊性。添加自己的元素p.abc,提高比.abc更高的特殊性。

在主体标签上添加类或ID
body.news{}
灵活的维护不同的页面

在注释中添加标志，能立即找到对应的部分
/*@group tyay*/

注意注释的逻辑结构。查询css结构获得更多。注释写清楚每个颜色的代码，可能更易读。

避免IE怪癖盒子模型。不要给元素添加具有指定宽度的内边距，而是尝试将内边距或外边距添加到元素的父元素或子元素上。

IE的盒子模型中的宽度包含了padding，为了防止这种情况发生。一般为本元素添加外边距，或者给父元素添加内边距。

![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d4)

外边距叠加。

只有普通文档流才会外边距叠加。**行内框、浮动框、绝对定位不会叠加。**

行内框inline水平间距，可以使用padding margin  border调整。但是垂直高度不受影响。给行内框显示的设置宽度和高度也没有效果。

由一行形成的水平框成为行框，行框的高度总是足以容纳包含的所有行内框。垂直高度只能用行高调整。

**修改行内框尺寸的方法，行高、水平padding、margin、border。**

display 可以设置inline-block,使得行内框赋有了block的行为。

绝对定位的元素的位置是相对于距离他最近的那个已经定位的祖先元素确定的。

浮动会让元素脱离文档流，不再影响不浮动的元素。但是浮动元素后面有一个文档流中的元素，那么这个元素的框就会表现的浮动根本不存在，但是框内的文本会给图片留出空间。

父框中的两个元素全部浮动，父框就会消失。避免这种方法的办法是，在两个元素下面加一个元素，使用clear。或者浮动整个父亲框。或者对父元素进行overflow:hidden,会自动清理内部浮元素。

更好的代码.因为被清理的元素在他们的顶外边距上添加了空间，所以生成的内容需要将他们的display属性设置为block
```css
.clear:after{
content:".";
height;0;
visibility:hidden;
display:block;
clear:both;
}
```

#背景图像效果
- 创建一个很窄的图像，然后横向平铺，底部过渡到一个颜色，然后背景色也使用这个颜色。
- 页面添加logo，可以弄一个div，大小是logo的大小。然后背景图片是logo，不平铺。

```css
h1{
padding-left:30px;
background-image:url(/img/bullet.gif);
background-repeat:no-repeat;
background-position: left center;
}
```
- 这是一个自定义项目符号的代码，利用padding空出空间。


- 如果使用百分比定位的话，图像上距离左上角20%的点定位到父元素上距离左上角20%的位置。

- 如果使用百分比定位上述案例。当然，后三条可以写成一行。
```css
h1{
padding-left:30px;
background-image:url(/img/bullet.gif);
background-repeat:no-repeat;
background-position: 0 50%;
}
```

- ![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d9)
不希望内容碰到边界，加额外的padding
```css
.box { 
  width: 418px; 
  background: #effce7 url(/img/bottom.gif) no-repeat  left bottom; 
  padding-bottom: 1px; 
} 
 
.box h2 { 
  background: url(/img/top.gif) no-repeat left top; 
  margin-top: 0; 
  padding: 20px 20px 0 20px; 
} 
 
.box p { 
  padding: 0 20px; 
} 
```

滑动门技术
![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d5)
- 

- 山顶角
- ![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d8)

- 为了不添加额外的元素，可以使用多背景
- ![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d7)

- border-radius 终极解决方案
- border-image ![](https://leanote.com/api/file/getImage?fileId=567e7353ab644164670074d3)

#投影
##简单投影
- 一个div中有一个image，用ps创造一个图层的阴影，如何应用呢？
```css
.img-wrapper { 
background: url(/img/shadow.gif) no-repeat bottom right; 
clear: right; 
float: left; 
} 
.img-wrapper img { 
margin: -5px 5px 5px -5px; 
} 
```
阴影应用于背景，右下角对齐。
因为div是块级元素，会水平伸展，占用可用空间. 浮动以后，会“收缩包围”到image上。要想露出图像，要把图像向左上移动，使用magin进行移动。

给图片加一个白边和一个黑框
```css
img{
	margin:-20px 20px 20px -20px;
	background-color: white;
	border:1px solid #a9a9a9;
	padding:4px;
}
```
要在IE6中实现需要把div的position变成relative，img的position变成relative、display变成block.

##相对定位的方法
```css
.img-wrapper { 
  background: url(/img/shadow.gif) no-repeat bottom right; 
  float:left; 
  line-height:0; 
} 
  
.img-wrapper img { 
  background:#fff; 
  padding:4px; 
  border:1px solid #a9a9a9; 
  position:relative; 
  left:-5px; 
  top:-5px; 
} 
```

##终极方法
```css
img { 
  -webkit-box-shadow: 3px 3px 6px #666; 
  -moz-box-shadow: 3px 3px 6px #666; 
  box-shadow: 3px 3px 6px #666; 
} 
```

注意，boxshadow和boxradius可以结合使用，制作出圆角的投影。

#不透明度
opacity:0.8;
filter:alpha(opacity=80); /ie/
- 使用RGBA可以设置不透明度rgba(0,0,0,0.8)
- 使用PNG图片，可以设置不透明度。
```css
<!--[if ie 6]> 
<link rel="stylesheet" type="text/css" href="ie6.css"/> 
<![endif]--> 
filter:progid:DXImageTransform.Microsoft.AlphaImageLoader 
(src=/img/my-image.png', sizingMethod='crop'); 
```
IE6支持不透明度的代码，而且需要只对IE6使用。

还有一种技术更为复杂
```css
img, div { 
   behavior: url(iepngfix.htc); 
} 
```


#视差
前景，中景，后景，设置不同的background-position
```css
body { 
  background-image: url(/img/bg-rear.jpg); 
  background-repeat: repeat-x; 
  background-color:#d3ff99; 
  background-position: 20% 0; 
} 
 
.midground { 
  background-image: url(/img/bg-mid.png); 
  background-repeat: repeat-x; 
  background-color: transparent; 
  background-position: 40% 0; 
} 
 
.foreground { 
  background-image: url(/img/bg-front.png); 
  background-repeat: repeat-x; 
  background-color: transparent; 
  background-position: 150% 0; 
} 
```

#文本替换
使用图片替换文本
```css
h2 { 
  text-indent: -5000px; 
  background:url(/img/hello_world.gif) no-repeat; 
  width: 150px; 
  height:35px; 
} 
```

SIFR方法替换，使用flash字体，具体百度

#超级链接

```css
a:link, a:visited {text-decoration: none;} 
a:hover, a:focus, a:active {text-decoration: underline;} 
```
注意顺序，这个顺序去掉下划线是可以的，反过来就不行了。

:target
用a定位后，选择目标文件。类似于维基百科的一小块。

用一个背景线条，在下方x重复，可以实现鼠标移动上去显示横线的一些效果。

这种外部链接样式怎么做的？

![](https://leanote.com/api/file/getImage?fileId=56809205ab6441660a00848c)

```css
a[href^="http:"] { 
  background: url(/img/externalLink.gif) no-repeat right top; 
  padding-right: 10px; 
} 
```
把他放在右上角即可，使用padding给出空间。同样的，也可以扩展。比如邮件是邮件的按钮，rss是rss的按钮。等等。

#创建类似按钮的链接
```css
a{
	display: block;
	width:6.6em;
	line-height:1.4;
	text-align: center;
	text-decoration: none;
	border: 1px solid #66a300;
	background-color: #8cca12;
	color:#fff;
}
```
链接是行内元素，只有单击内容才能激活，有更大的点击区域，应怪把display设置成block。块级元素会扩展宽度，如果父级元素限定了宽度，就不需要为链接宽度担心。高度用line-height可以让文本垂直居中。

##链接的翻转
就是使用hover 鼠标移动上去，背景图片变色。

- pixy样式翻转，使用一个大图，分别应用不同的小图
```css
a{
background:url(abc.jpg) -100px -200px
}
```
但是，ie会闪烁。因此，要应用于父级图像，才会不闪烁。比如应用于a外的li。li中是一直显示的，只不过被a盖住了。闪烁的时候，a就没了，就显示出了li，然后a一下就出来了，li就又被盖住了

对ie使用缓存技术，可以不让他重新加载的时候闪烁。
```css
html { 
  filter: expression(document.execCommand("BackgroundImageCache",« 
false, true)); 
} 
```

创建个CSS按钮，自己慢慢研究，就是加了阴影圆角和倒影
```css
a { 
display: block; 
width: 6.6em; 
  height: 1.4em; 
  line-height: 1.4; 
  text-align: center; 
  text-decoration: none; 
  border: 1px solid #66a300; 
   -moz-border-radius: 6px; 
   -webkit-border-radius: 6px; 
   border-radius: 6px; 
  background-image: -webkit-gradient(linear, left top, left bottom, « 
from(#abe142), to(#67a400)); 
  background-color: #8cca12; 
   color: #fff; 
  text-shadow: 2px 2px 2px #66a300; 
  -moz-box-shadow: 2px 2px 2px #ccc; 
  -webkit-box-shadow: 2px 2px 2px #ccc; 
  box-shadow: 2px 2px 2px #ccc; 
  -webkit-box-reflect: below 2px -webkit-gradient«  
(linear, left top, left bottom, from(transparent),«  
color-stop(0.52, transparent), to(white)); 
} 
```

链接提示
```css
a{position: relative;}
span{display: none;}
a:hover span{
	display: block;
	position: absolute;
	top:1em;
	left: 2em;
	padding: 0.2em 0.6em;
	border: 1px solid #996633;
	background-color: #ffff66;
	color: #000;
}
```
span外面有个a，先不让span显示。当鼠标移动到a上的时候，再显示。进行绝对定位的位移，需要把父元素a设置成相对定位。

##创建一个垂直菜单
![](https://leanote.com/api/file/getImage?fileId=56815548ab644164670085f2)
```html
<ul class="nav"> 
  <li><a href="home.htm">Home</a></li> 
  <li><a href="about.htm">About</a></li> 
  <li><a href="services.htm">Our Services</a></li> 
  <li><a href="work.htm">Our Work</a></li> 
  <li><a href="news.htm">News</a></li> 
  <li><a href="contact.htm">Contact</a></li> 
</ul> 
```

```css
ul.nav { 
  margin: 0; 
  padding: 0; 
  list-style-type: none; 
  width: 8em; 
  background-color: #8BD400; 
  border: 1px solid #486B02; 
} 
ul.nav a { 
  display: block; 
  color: #2B3F00; 
  text-decoration: none; 
  border-top: 1px solid #E4FFD3; 
  border-bottom: 1px solid #486B02; 
  /* 上下颜色不一样 产生凹槽效果 */ 
  background: url(/img/arrow.gif) no-repeat 5% 50%; 
  padding: 0.3em 1em; 
} 
ul.nav .last a { 
  border-bottom: 0; 
  /* 最后一个恢复 */ 
} 
ul.nav a:hover, 
ul.nav a:focus, 
  ul.nav .selected a { 
  color: #E4FFD3; 
  background-color: #6DA203; 
} 
ul.nav li { 
  display: inline: /* :KLUDGE: Removes large gaps in IE/Win */ 
} 
```
IE6在列表下增加了额外的空间，需要用inline修复。

##在导航中突出显示当前页面
```html
<body id="home"> 
<ul class="nav"> 
  <li><a href="home.htm">Home</a></li> 
  <li><a href="about.htm">About</a></li> 
  <li><a href="services.htm">Our Services</a></li> 
  <li><a href="work.htm">Our Work</a></li> 
  <li><a href="news.htm">News</a></li>
    <li><a href="contact.htm">Contact</a></li> 
</ul> 
</body> 
```
```css
#home .nav .home a, 
#about .nav .about a , 
#news .nav .news a, 
#products .nav .products a, 
#services .nav .services a { 
  background-position: right bottom; 
  color: #fff; 
  cursor: default; 
} 
```

如何做出这个东西呢
![](https://leanote.com/api/file/getImage?fileId=56815548ab644164670085f1)

```css
ol.pagination { 
  margin: 0; 
  padding: 0; 
  list-style-type: none; 
} 
ol.pagination li { 
  float: left; 
  margin-right: 0.6em; 
} 
ol.pagination a, 
 ol.pagination  li.selected { 
  display: block; 
  padding: 0.2em 0.5em; 
  border: 1px solid #ccc; 
  text-decoration: none; 
} 
ol.pagination a:hover,  
ol.pagination a:focus, 
ol.pagination li.selected { 
  background-color: blue; 
  color: white; 
} 
ol.pagination a[rel="prev"], 
ol.pagination a[rel="next"] { 
  border: none; 
} 
ol.pagination a[rel="prev"]:before { 
  content: "\00AB"; 
  padding-right: 0.5em; 
} 
 
ol.pagination a[rel="next"]:after { 
  content: "\00BB"; 
  padding-left: 0.5em; 
} 
```

主要看prev前面和后面的制作方法。
#创建图形化导航
```css
ul.nav { 
  margin: 0; 
  padding: 0; 
  list-style: none; 
  width: 72em; 
  overflow: hidden; 
  background: #FAA819 url(img/mainNavBg.gif) repeat-x; 
} 
ul. nav li { 
  float: left; 
} 
ul.nav a { 
  display: block; 
  padding: 0 2em; 
  line-height: 2.1em; 
  background: url(img/divider.gif) repeat-y left top; 
  text-decoration: none; 
  color: #fff; 
} 
ul. nav .first a { 
  background-image: none; 
} ie6支持
ul.nav li:first-child a { 
  background: none; 
}  ie6不支持
ul.nav a:hover, 
ul.nav a:focus  { 
  color: #333; 
} 
```
每个导航的宽度是有文本大小决定的。不显示的设置宽度。

#采用拉伸门技术的水平导航菜单
![](https://leanote.com/api/file/getImage?fileId=5681dfddab6441660a008c38)
先放html代码
```html
<ul class="nav"> 
  <li><a href="home.htm">Home</a></li> 
  <li><a href="about.htm">About</a></li> 
  <li><a href="news.htm">News</a></li> 
  <li><a href="products.htm">Products</a></li> 
  <li><a href="services.htm">Services</a></li> 
  <li><a href="clients.htm">Clients</a></li> 
  <li><a href="case-studies.htm">Case Studies</a></li> 
</ul> 
```

再说CSS代码
```css
ul.nav { 
  margin: 0; 
  padding: 0; 
  list-style: none; 
  width: 72em; 
  overflow: hidden; 
} 
ul.nav li { 
  float: left; 
  background: url(img/tab-right.gif) no-repeat right top; 
} 
ul.nav li a { 
  display: block; 
  padding: 0 2em; 
  line-height: 2.5em; 
  background: url(img/tab-left.gif) no-repeat left top; 
  text-decoration: none; 
  color: #fff; 
  float: left; 
} 
ul.nav a:hover, 
ul.nav a:focus  { 
  color: #333; 
} 
```
- 几点注意，a也要浮动，解决ie5的兼容性问题。li要浮动，如果是a浮动，那么就没有li了。ul要displaynone，这样就不会收缩了。
-
-

#布局
##固定列宽布局
整体居中代码
```css
	.wrapper{
		width: 960px;
		margin: 0 auto;
		text-align: left;
	}
	body{
		text-align: center;
	}
```
左右各自浮动
```css
.primary{
		width: 650px;
		float: right;
		display: inline;
		background-color: blue;
		padding-right: 20px;
	}
	.secondary{
		width: 230px;
		float: left;
		display: inline;
		background-color: yellow;
	}
	.content{
		overflow: hidden;
	}
```

![](https://leanote.com/api/file/getImage?fileId=5683de61ab6441660a009980)

浮动的dispalay为inline可以ie兼容性

#流式布局
所有的宽度都设置成百分比，wrapper设置max-width：125em和min-width:62em. 窗口会随着百分比增大缩小。

#弹性布局
弹性布局相对于字号设置宽度。
```css
body{
    font-size:62.5%; 默认字体16px，这时候默认字体变成10px
}
wrapper{
    width:92em;
    max-width:95%
}
```
其他内部全部使用以前的百分比。

#图片弹性
使用背景图片。
使用元素图片。width:100%  overflow:hidden;

#faux列
对于侧边栏没法背景延伸到底部，可以在父级元素上设置一个背景y填充。

# 表单
```css
fieldset{
            margin: 1em 0;
            padding: 1em;
            border: 1px solid #ccc;
            background: #f8f8f8;
        }
        legend{
            font-weight: bold;
        }
        lable{
            display: block;
            cursor:pointer;
        }
        input[type="text"]{
            width: 20em;
        }
        textarea{
            width: 100%;
            height: 10em;
        }
        input.radio, input.checkbox, input.submit{
            width:auto;
        }
```

```html
    <fieldset>
        <legend>this is title</legend>
        <div>
            <lable for="author">Name:</lable>
            <input type="text" id="author" name="author">
        </div>
        <div>
            <lable for="email">email:</lable>
            <input type="text" id="email" name="email">
        </div>

    </fieldset>
```

横向的布局，浮动lable，给lable设定宽度。