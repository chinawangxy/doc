### 清除浮动

> 浮动给我们的代码带来的麻烦，想必不需要多说，我们会用很多方式来避免这种麻烦，其中我觉得最方便也是兼容性最好的一种是，在同级目录下再创建一个<div style="clear:both;"></div>；不过这样会增加很多无用的代码。此时我们用:after 这个伪元素来解决浮动的问题，如果当前层级有浮动元素，那么在其父级添加上 clearfix 类即可。

```
清除浮动
.clearfix:after {
    content: "\00A0";
    display: block;
    visibility: hidden;
    width: 0;
    height: 0;
    clear: both;
    font-size: 0;
    line-height: 0;
    overflow: hidden;}
.clearfix {  zoom: 1;}
```

### 垂直水平居中

> 在 css 的世界里水平居中比垂直居中来的简单一些，经过了多年的演化，依然没有好的方式来让元素垂直居中(各种方式各有优缺点，但都不能达到兼容性好，破坏力小的目标)，以下是几种常见的实现方式

```
// 绝对定位方式且宽高已知
position: absolute;
top: 50%;
left: 50%;
margin-top: -3em;
margin-left: -7em;
width: 14em;
height: 6em;
```

```
// 绝对定位 + 未知宽度 + translate
position: absolute;
left: 50%;
top: 50%;
transform: translate(-50%, -50%);
//需要补充浏览器前缀
```

```
// flex 轻松搞定水平垂直居中(未知宽高)

display: flex;
align-items: center;
justify-content: center;
```

### 文本末尾添加省略号

> 当文本的内容超出容器的宽度的时候，我们希望在其默认添加省略号以达到提示用户内容省略显示的效果。

```
// 宽度固定，适合单行显示...

overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

```
// 宽度不固定，适合多行以及移动端显示
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 3;
-webkit-box-orient: vertical;
```

### 制造文本的模糊效果

> 当我们希望给文本制造一种模糊效果感觉的时候，可以这样做

```
color: transparent;
text-shadow: 0 0 2px rgba(0, 0, 0, 0.5);

```

### 动画实现简洁 loading 效果

> 我们来实现一个非常简洁的 loading 效果

```
.loading:after {
  display: inline-block;
  overflow: hidden;
  vertical-align: bottom;
  content: "\2026";
  -webkit-animation: ellipsis 2s infinite;
}

// 动画部分
@-webkit-keyframes ellipsis {
  from {
    width: 2px;
  }
  to {
    width: 15px;
  }
}
```

### 自定义文本选中样式

> 默认情况下，我们在网页上选中文字的时候，会给选中的部分一个深蓝色背景颜色(可以自己拿起鼠标试试)，如果我们想自己定制被选中的部分的样式呢？

```
// 注意只能修改这两个属性 字体颜色 选中背景颜色

element::selection {
  color: green;
  background-color: pink;
}
element::-moz-selection {
  color: green;
  background-color: pink;
}
```

### 顶角贴纸效果

> 有时候我们会有这样的需求，在一个列表展示页面，有一些列表项是新添加的、或者热度比较高的，就会要求在其上面添加一个贴纸效果的小条就像 hexo 默认博客的 fork me on github 那个效果一样。

```
<div class="wrap">
  <div class="ribbon">
    <a href="#">Fork me on GitHub</a>
  </div>
</div>

/* 外层容器几本设置  */
.wrap {
  width: 160px;
  height: 160px;
  overflow: hidden;
  position: relative;
  background-color: #f3f3f3;
}

.ribbon {
  background-color: #a00;
  overflow: hidden;
  white-space: nowrap;
  position: absolute;
  /* shadom */
  -webkit-box-shadow: 0 0 10px #888;
  -moz-box-shadow: 0 0 10px #888;
  box-shadow: 0 0 10px #888;
  /* rotate */
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  -ms-transform: rotate(-45deg);
  -o-transform: rotate(-45deg);
  transform: rotate(-45deg);
  /* position */
  left: -50px;
  top: 40px;
}

.ribbon a {
  border: 1px solid #faa;
  color: #fff;
  display: block;
  font: bold 81.25% "Helvetica Neue", Helvetica, Arial, sans-serif;
  margin: 1px 0;
  padding: 10px 50px;
  text-align: center;
  text-decoration: none;
  /* shadow */
  text-shadow: 0 0 5px #444;
}
```

### input 占位符

> 当我们给部分 input 类型的设置 placeholder 属性的时候，有的时候需要修改其默认的样式。

```

input::-webkit-input-placeholder {
  color: green;
  background-color: #f9f7f7;
  font-size: 14px;
}
input::-moz-input-placeholder {
  color: green;
  background-color: #f9f7f7;
  font-size: 14px;
}
input::-ms-input-placeholder {
  color: green;
  background-color: #f9f7f7;
  font-size: 14px;
}
```

### 移动端可点击元素去处默认边框

> 在移动端浏览器上，当你点击一个链接或者通过 Javascript 定义的可点击元素的时候，会出现蓝色边框，说实话，这是很恶心的，怎么去掉呢?

```
-webkit-tap-highlight-color: rgba(255, 255, 255, 0);

```

### 首字下沉

> 要实现类似 word 中首字下沉的效果可以使用以下代码

```
element:first-letter {
  float: left;
  color: green;
  font-size: 30px;
}
```

### 小三角

> 在很多地方我们可以用得上小三角，接下来我们画一下四个方向的三角形。

```
.triangle {
  /* 基础样式 */
  border: solid 10px transparent;
}
/*下*/
.triangle.bottom {
  border-top-color: green;
}
/*上*/
.triangle.top {
  border-bottom-color: green;
}
/*左*/
.triangle.top {
  border-right-color: green;
}
/*右*/
.triangle.top {
  border-left-color: green;
}

```

### 鼠标手型

> 一般情况下，我们希望在以下元素身上添加鼠标手型
> a
> submit
> input[type="iamge"]
> input[type="button"]
> button
> label
> select

```
a[href],
input[type="submit"],
input[type="image"],
input[type="button"],
label[for],
select,
button {
  cursor: pointer;
}
```

### 屏蔽 Webkit 移动浏览器中元素高亮效果

> 在访问移动网站时，你会发现，在选中的元素周围会出现一些灰色的框框，使用以下代码屏蔽这种样式

```
-webkit-touch-callout: none;
-webkit-user-select: none;
-khtml-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
```

### 移除常用标签的浏览器默认的 margin 和 padding

> pre、code、legend、fieldset、blockquote … 等标签不是很常用，所以就不一一列举，如果项目中使用到，可以自己单独写

```

body,
p,
h1,
h2,
h3,
h4,
h5,
h6,
dl,
dd,
ul,
ol,
th,
td,
button,
figure,
input,
textarea,
form {
  margin: 0;
  padding: 0;
}
```

### 统一 input、select、textarea 宽度

> 不同浏览器的 input、select、textarea 的盒子模型宽度计算方式不同，统一为最常见的 content-box。

```
input,
select,
textarea {
  -webkit-box-sizing: content-box;
  -moz-box-sizing: content-box;
  box-sizing: content-box;
}

table {
  /*table 相邻单元格的边框间的距离设置为 0*/
  border-spacing: 0;
  /*默认情况下给 tr 设置 border 没有效果，如果 table 设置了边框为合并模式：「border-collapse: collapse;」就可以了*/
  border-collapse: collapse;
}
```

### 移除浏览器部分元素的默认边框

> acronym、fieldset … 等其他标签不是很常用，就不会一一列举；如果项目中用到，可以自己单独写。

```
img,
input,
button,
textarea {
  border: none;
  -webkit-appearance: none;
}

input {
  /*由于 input 默认不继承父元素的居中样式，所以设置：「text-align: inherit」*/
  text-align: inherit;
}

textarea {
  /*textarea 默认不可以放缩*/
  resize: none;
}
```

### 取消元素 outline 样式

> 由于以下元素的部分属性没有继承父节点样式，所以声明这些元素的这些属性为父元素的属性。

```
a,
h1,
h2,
h3,
h4,
h5,
h6,
input,
select,
button,
option,
textarea,
optgroup {
  font-family: inherit;
  font-size: inherit;
  font-weight: inherit;
  font-style: inherit;
  line-height: inherit;
  color: inherit;
  outline: none;
}
```

### 取消超链接元素的默认文字装饰

> 另外 del、ins 标签的中划线、下划线还是挺好的，就不去掉

```
a {
  text-decoration: none;
}

ol,
ul {
  /*开发中 UI 设计的列表都是和原生的样式差太多，所以直接给取消 ol，ul 默认列表样式*/
  list-style: none;
}

button,
input[type="submit"],
input[type="button"] {
  /*鼠标经过是「小手」形状表示可点击*/
  cursor: pointer;
}

input::-moz-focus-inner {
  /*取消火狐浏览器部分版本 input 聚焦时默认的「padding、border」*/
  padding: 0;
  border: 0;
}
```

### 取消部分浏览器数字输入控件的操作按钮

```
input[type="number"] {
  -moz-appearance: textfield;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  margin: 0;
  -webkit-appearance: none;
}
```

### 输入控件 placeholder 色设置 #999

```
input::-webkit-input-placeholder,
textarea::-webkit-input-placeholder {
  color: #999;
}

input:-moz-placeholder,
textarea:-moz-placeholder {
  color: #999;
}

input::-moz-placeholder,
textarea::-moz-placeholder {
  color: #999;
}

input:-ms-input-placeholder,
textarea:-ms-input-placeholder {
  color: #999;
}

template {
  /*由于部分浏览 template 会显示出来，所以要隐*/
  display: none;
}

```

### position: fixed 的缩写

```
.pf {
  position: fixed;
  /*chrome 内核 浏览器 position: fixed 防止抖动*/
  -webkit-transform: translateZ(0);
}
```

### 利用绝对定位宽高拉升原理，中心居中元素

```
.middle {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;
}
```

### 利用相对定位于 CSS3 使元素垂直居中

```
.v-middle {
  position: relative;
  top: 50%;
  -webkit-transform: -webkit-translateY(-50%);
  -moz-transform: -moz-translateY(-50%);
  -o-transform: -o-translateY(-50%);
  transform: translateY(-50%);
}
```

### 元素计算宽高的盒子模型以 border 为外界限「bb ==> border-box」

```
.bb {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

### 单行文本溢出显示省略号「to ==> text-overflow」

```
.to {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

### 初始化样式

> 不同的浏览器对各个标签默认的样式是不一样的，而且有时候我们也不想使用浏览器给出的默认样式，我们就可以用 reset.css 去掉其默认样式

```
body,
h1,
h2,
h3,
h4,
h5,
h6,
hr,
p,
blockquote,
dl,
dt,
dd,
ul,
ol,
li,
pre,
form,
fieldset,
legend,
button,
input,
textarea,
th,
td {
  margin: 0;
  padding: 0;
}
body,
button,
input,
select,
textarea {
  font: 12px/1.5 tahoma, arial, \5b8b\4f53;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: 100%;
}
address,
cite,
dfn,
em,
var {
  font-style: normal;
}
code,
kbd,
pre,
samp {
  font-family: couriernew, courier, monospace;
}
small {
  font-size: 12px;
}
ul,
ol {
  list-style: none;
}
a {
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
sup {
  vertical-align: text-top;
}
sub {
  vertical-align: text-bottom;
}
legend {
  color: #000;
}
fieldset,
img {
  border: 0;
}
button,
input,
select,
textarea {
  font-size: 100%;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```

### 强制换行/自动换行/强制不换行

```

/* 强制不换行 */
div {
  white-space: nowrap;
}

/* 自动换行 */
div {
  word-wrap: break-word;
  word-break: normal;
}

/* 强制英文单词断行 */
div {
  word-break: break-all;
}


```

### table 边界的样式

```

table {
  border: 1px solid #000;
  padding: 0;
  border-collapse: collapse;
  table-layout: fixed;
  margin-top: 10px;
}
table td {
  height: 30px;
  border: 1px solid #000;
  background: #fff;
  font-size: 15px;
  padding: 3px 3px 3px 8px;
  color: #000;
  width: 160px;
}
```

### 绝对定位与 margin

> 当我们提前知道要居中元素的长度和宽度时，可以使用这种方式：

```
.container {
  position: relative;
  width: 300px;
  height: 200px;
  border: 1px solid #333333;
}
.content {
  background-color: #ccc;
  width: 160px;
  height: 100px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -80px; /* 宽度的一半 */
  margin-top: -50px; /* 高度的一半 */
}

```

### 绝对定位与 transform

> 当要居中的元素不定宽和定高时，我们可以使用 transform 来让元素进行偏移。

```
.container {
  position: relative;
  width: 300px;
  height: 200px;
  border: 1px solid #333333;
}
.content {
  background-color: #ccc;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate3d(-50%, -50%, 0);
  text-align: center;
}
```

### 标题两边的小横杠

> 我们经常会遇到这样的 UI 需求，就是标题两边有两个小横岗，之前是怎么实现的呢？比如用个 border-top 属性，然后再把中间的文字进行绝对定位，同时给这个文字一个背景颜色，把中间的这部分盖住。

```
<div class="title">标题</div>
title {
  color: #e1767c;
  font-size: 0.3rem;
  position: relative;

  &:before,
  &:after {
    content: "";
    position: absolute;
    display: block;
    left: 50%;
    top: 50%;
    -webkit-transform: translate3d(-50%, -50%, 0);
    transform: translate3d(-50%, -50%, 0);
    border-top: 0.02rem solid #e1767c;
    width: 0.4rem;
  }
  &:before {
    margin-left: -1.2rem;
  }
  &:after {
    margin-left: 1.2rem;
  }
}

```

###浮动类

> 常规浮动 list 浮动 image 浮动

```
.float-left {
  float: left;
}
.float-right {
  float: right;
}
.float-li li,/*定义到li父元素或祖先元素上*/ li.float-li {
  float: left;
}
.float-img img,/*定义到img父元素或祖先元素上*/ img.float-li {
  float: left;
}
.float-span span,/*定义到span父元素或祖先元素上*/ span.float-span {
  float: right;
}
```

### 背景图片嵌入与定位

```
.bg-img {
  background-image: url("../img/bg.png");
  background-position: center top;
  background-repeat: no-repeat;
}
.bg01-img {
  background-image: url("../img/bg01.png");
  background-position: center top;
  background-repeat: no-repeat;
}
.bg02-img {
  background-image: url("../img/bg02.png");
  background-position: center top;
  background-repeat: no-repeat;
}
.bg03-img {
  background-image: url("../img/bg03.png");
  background-position: center top;
  background-repeat: no-repeat;
}
.bg04-img {
  background-image: url("../img/bg04.png");
  background-position: center top;
  background-repeat: no-repeat;
}

```

### 继承类

```

.inherit-width {
  width: inherit;
}
.inherit-min-width {
  min-width: inherit;
}
.inherit-height {
  height: inherit;
}
.inherit-min-height {
  min-height: inherit;
}
.inherit-color {
  color: inherit;
}
```

### 文本缩进

```

.text-indent {
  text-indent: 2rem;
}
/*16px*/
.text-indent-xs {
  text-indent: 1.5rem;
}
/*12px*/
.text-indent-sm {
  text-indent: 1.7rem;
}
/*14px*/
.text-indent-md {
  text-indent: 2rem;
}
/*18px*/
.text-indent-lg {
  text-indent: 2.4rem;
}
/*20px*/
```

### 行高

```
.line-height-xs {
  line-height: 1.3rem;
}
.line-height-sm {
  line-height: 1.5rem;
}
.line-height-md {
  line-height: 1.7rem;
}
.line-height-lg {
  line-height: 2rem;
}

.line-height-25x {
  line-height: 25px;
}
.line-height-30x {
  line-height: 30px;
}
```

### ul 缩进

```

.ul-indent-xs {
  margin-left: 0.5rem;
}
.ul-indent-sm {
  margin-left: 1rem;
}
.ul-indent-md {
  margin-left: 1.5rem;
}
.ul-indent-lg {
  margin-left: 2rem;
}
.ol-list,
.ul-list {
  list-style: disc;
}
```

### 文本截断

```

.truncate {
  max-width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.hide {
  display: none;
}
```

### 图片、视频规范

```
.img-max,
.video-max {
  width: 100%;
  height: auto;
}
/*display显示方式*/
.inline {
  display: inline;
}
.inline-block {
  display: inline-block;
}
.block {
  display: block;
}
```

### 分割线预设

```
hr,
.hr-xs-Silver,
.hr-sm-black,
.hr-sm-Silver,
.hr-xs-gray,
.hr-sm-gray {
  margin: 20px 0;
}
hr {
  border: none;
  border-top: 1px solid #000;
}
.hr-xs-Silver {
  border: none;
  border-top: 1px solid #c0c0c0;
}
.hr-sm-black {
  border: none;
  border-top: 2px solid #000;
}
.hr-sm-Silver {
  border: none;
  border-top: 2px solid #c0c0c0;
}
.hr-xs-gray {
  border: none;
  border-top: 1px solid #767676;
}
.hr-sm-gray {
  border: none;
  border-top: 2px solid #767676;
}
```

### 鼠标 a 标签 hover 效果

```
.hover-red a:hover,/*为a标签祖先元素添加类名 默认无智能提醒*/ a.hover-red:hover {
  color: red;
} /*单独为a标签添加类名*/
.hover-yellow a:hover,/*为a标签祖先元素添加类名 默认无智能提醒*/ a.hover-yellow:hover {
  color: #ffd700;
} /*单独为a标签添加类名*/
.hover-green a:hover,/*为a标签祖先元素添加类名 默认无智能提醒*/ a.hover-green:hover {
  color: #70aa39;
} /*单独为a标签添加类名*/
.hover-blue a:hover,/*为a标签祖先元素添加类名 默认无智能提醒*/ a.hover-blue:hover {
  color: blue;
} /*单独为a标签添加类名*/
.hover-gray a:hover,/*为a标签祖先元素添加类名 默认无智能提醒*/ a.hover-gray:hover {
  color: #9c9c9c;
} /*单独为a标签添加类名*/
.underline a:hover,
a.underline:hover {
  text-decoration: underline;
}

```

### 阴影效果

```

.shadow-text-xs {
  text-shadow: 4px 3px 0 #1d9d74, 9px 8px 0 rgba(0, 0, 0, 0.15);
} /*智能兼容ie10以上 暂不考虑*/

.shadow-xs {
  -ms-filter: "progid:DXImageTransform.Microsoft.Shadow(Strength=1, Direction=100, Color='#cccccc')"; /* For IE 8 */
  filter: progid:DXImageTransform.Microsoft.Shadow(Strength=1, Direction=100, Color='#cccccc'); /* For IE 5.5 - 7 */
  -moz-box-shadow: 1px 1px 2px #cccccc; /* for firefox */
  -webkit-box-shadow: 1px 1px 2px #cccccc; /* for safari or chrome */
  box-shadow: 1px 1px 2px #cccccc; /* for opera or ie9 */
}
.shadow-sm {
  -ms-filter: "progid:DXImageTransform.Microsoft.Shadow(Strength=2, Direction=120, Color='#cccccc')"; /* For IE 8 */
  filter: progid:DXImageTransform.Microsoft.Shadow(Strength=2, Direction=120, Color='#cccccc'); /* For IE 5.5 - 7 */
  -moz-box-shadow: 2px 2px 3px #cccccc; /* for firefox */
  -webkit-box-shadow: 2px 2px 3px #cccccc; /* for safari or chrome */
  box-shadow: 2px 2px 3px #cccccc; /* for opera or ie9 */
}
.shadow-md {
  -ms-filter: "progid:DXImageTransform.Microsoft.Shadow(Strength=3, Direction=135, Color='#cccccc')"; /* For IE 8 */
  filter: progid:DXImageTransform.Microsoft.Shadow(Strength=3, Direction=135, Color='#cccccc'); /* For IE 5.5 - 7 */
  -moz-box-shadow: 3px 3px 5px #cccccc; /* for firefox */
  -webkit-box-shadow: 3px 3px 5px #cccccc; /* for safari or chrome */
  box-shadow: 3px 3px 5px #cccccc; /* for opera or ie9 */
}
.shadow-lg {
  -ms-filter: "progid:DXImageTransform.Microsoft.Shadow(Strength=5, Direction=150, Color='#cccccc')"; /* For IE 8 */
  filter: progid:DXImageTransform.Microsoft.Shadow(Strength=5, Direction=150, Color='#cccccc'); /* For IE 5.5 - 7 */
  -moz-box-shadow: 5px 5px 8px #cccccc; /* for firefox */
  -webkit-box-shadow: 5px 5px 8px #cccccc; /* for safari or chrome */
  box-shadow: 5px 5px 8px #cccccc; /* for opera or ie9 */
}
```

### 圆角

```

.border-radius-xs {
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  border-radius: 3px;
}
.border-radius-sm {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
.border-radius-md {
  -webkit-border-radius: 7px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
.border-radius-lg {
  -webkit-border-radius: 9px;
  -moz-border-radius: 9px;
  border-radius: 9px;
}
```
