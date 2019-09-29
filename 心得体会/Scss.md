# Scss

首先要了解什么是CSS 预处理器？ SCSS是一种CSS预处理语言

  定义了一种新的专门的编程语言，编译后形成正常的css文件，为css增加一些编程特性，无需考虑浏览器的兼容性（完全兼容css3），让css更加简洁、适应性更强，可读性更佳，更易于代码的维护等诸多好处。CSS预处理语言有SCSS (SASS) 和LESS、POSTCSS

 

那么SCSS和SASS 有什么区别呢

· 文件扩展名不同，文件后缀分别是“.scss”和“.sass”

· sass是以严格缩进语法规则来编写代码的，不包括大括号和分号，而scss的语法和css书写语法类似；sass的安装和使用不细说了；

· scss是sass3.0引入的语法，可以理解scss是sass的一个升级版本，是一种SCSS-like语言，弥补了sass和css之间的鸿沟；

 

 

这篇文章是记录的在VUE项目中SCSS的使用

 

vue项目上安装SCSS和开发入门

 

① 使用vue-cli模板创建新项目：vue init webpack myvue

② 安装sass 依赖包 ，在cmd界面输入：

npm  install sass-loader --save-dev
npm install node-sass --sava-dev

③ 在build文件夹下的webpack.base.conf.js的rules里面添加配置

{
test: /\.scss$/,
loaders: ['style', 'css', 'sass']
}
④ 使用scss时候在所在的style样式标签上添加lang=”scss”即可应用对应的语法，否则报错

⑤ scss使用测试：如下测试修改字体颜色

<style lang="scss">
$color:red;
div {color:$color;}
</style>

 

 

 

 

 

那么进一步了解SCSS 的使用语法 ??

SCSS语法：

·注释

注释分为三种：/* */css中显示，//css中不显示，/*重要注释!*/压缩不会被删掉。

 

·@import 命令导入外部sass、scss、css文件

<style lang="scss">
@import './test.scss'; //导入外部scss文件
.myText {
   border:1px solid red;
}
</style>

 

·变量

声明变量的语法是：$+变量名+：+变量值；如下

$color:red; //声明变量 $color

 

区分默认变量

默认变量只需要在变量值后加上 !default , 用来设置默认值 ，对默认变量进行重新声明可以实现覆盖默认值；如

$color:red !default; //声明默认变量 $color
$color:purple; //根据需求覆盖默认变量
.father01 {
   color:$color;
}

区分全局变量和局部变量

全局变量是元素外声明的变量，局部变量是在元素里声明的变量，重复声明时局部变量会覆盖全局变量；

 

$height:200px; //全局变量声明不在大花括号内
$bgcolor:blue;
body {
   .father01 {  //嵌套
​      width:$width;
​      height:$height;
​      $border:1px solid red; //局部变量是声明在元素内的
​      border: $border;
​      $bgcolor:purple; //全局变量和局部变量名一致时，调用局部变量进行覆盖
​      background-color: $bgcolor;
   }
}

局部变量值后加上 !global 关键词可以使得局部变量变成全局变量；

 

body {
   .father01 {
​      width:200px;
​      height:200px;
​      $border:1px solid red !global; //使用global关键词将$border变为了全局变量
​      border:$border;
   }
   .father02 {
​      width: 300px;
​      height:300px;
​      border:$border; //使用全局变量
   }
}

 

·变量嵌套引用：即字符串插值，需要使用 #{} 来进行包裹

 

$left:left;
.father02 {
   width: 300px;
   height:300px;
   border:$border; //使用全局变量
border-#{$left}:2px solid purple; //使用字符串插值之前必须先声明
}

 

·变量计算

$left:left;
.father02 {
   width: 300px;
   height:300px;
   border:$border; //使用全局变量
border-#{$left}:2px solid purple; //使用字符串插值之前必须先声明
}

 

·嵌套

  选择器嵌套不多说了

属性嵌套（有相同属性前缀）如下

border:{
   color:red;
   width:5px;
   style:solid;
}

在嵌套时候可以使用 & 来引用父元素

 

.container {
   &>p {   //可以编译成CSS的 .container>p {} 效果
​      color:purple;
   }
}

 

·继承

 继承 .class 使用 @extend

.container {
   color:purple;
   border:2px dashed purple;
}
.myText {
   @extend .container; //这里将继承.container类的所有样式
   font-size: 22px;
}

 

·SCSS占位符 %

使用% 声明的代码块，如果不被@extend调用的话就不会被编译。编译出来的代码会将相同的代码合并在一起，代码变得十分简洁。

%m5 { background-color: lightblue;}
.P1 { @extend %m5; }

 

·重复代码块，使用混合@mixin命令定义，以及使用@include调用该mixin

 

@mixin normalStyle {
   //使用@mixin命令定义可重复使用的代码块
   width:300px;
   height:100px;
   color:black;
   background-color:lightblue;
}
.container {
   @include normalStyle;
   //使用@include 命令引用@mixin定义的代码块
}

 在使用@mixin和@include时，传入参数和默认值

@mixin normalStyle($width,$height,$color,$defaultValue:orange) {
   width:$width;
   height:$height;
   color:$color;
   background-color:$defaultValue;
}
.container {
   @include normalStyle(300px,100px,green,lightgray);
}

SCSS使用编程式方法 

·条件语句 

.container {
   p {
​      @if 1+1<3 {
​         border:1px solid blue;
​      } @else {
​         border:1ps dashed palevioletred;
​      }
   }
}

 

·SCSS中的三种循环

 

for循环

在sass中的@for循环有两种方式：

①@for $i from <start> through <end>

②@for $i from <start> to <end>

其中$i表示变量，start表示开始值，end表示结束值；

through表示包括end这个数值；to表示不包括end这个数值；

 

while循环

只要@while后面的条件为true就会执行，直到表达式值为false时停止循环；

 

each  in循环

就是去遍历一个列表，然后从列表中取出对用值；他的指令形式为：@each $var in <list>($var为变量值，list为sassscript表达式）

//for 循环
@for $i from 1 to 5 {
   .item-#{$i} {
​      border:#{$i}px solid;
   }
}
//while 循环
$m:8;
@while $m > 0 {
   .items-#{$m} {
​      width:2em*$m;
   }
   $m:$m - 2 ;
}
//这里可以对$m进行运算 让它每次都减去2
//each 语法
@each $item in class01,class02 { //$item就是遍历了in关键词后面的类名列
   .#{$item} {
​      background-color:purple;
   }
}
//会编译成 .class01 , .class02 {background-color:purple;}

 

·使用@function 自定义函数及使用

@function double($sn){ //SCSS允许自定义函数
   @return $sn*2;
}
.myText {
   border:1px solid red;
   width:double(200px); //使用在SCSS中自定义的函数
}

 

·可以直接使用SCSS内置的颜色函数，

.myText {
   color:black;
   &:hover{
​      //以下的lighten()、darken()等是SCSS内置的颜色函数
​      color:lighten(#cc3, 10%); // #d6d65c颜色变浅
​      color:darken(#cc3, 10%); // #a3a329颜色加深
​      color:grayscale(#cc3); // #d6d65c
​      color:complement(#cc3); // #a3a329
   }
}





# [SCSS & SASS Color 颜色函数用法](https://www.cnblogs.com/kaiye/p/7553041.html)

最近做一个没有设计师参与的项目，发现 scss 内置的颜色函数还挺好用。记录分享下

## rgba() 

能省掉手工转换 hex 到 rgb 格式的工作，如以下 SCSS 代码

```
$linkColor: #20a0ff;

.box{
  box-shadow: 0 2px 6px 0 rgba($linkColor, 0.3);
  background-color: $linkColor;
}
```

生成的 CSS 代码

```
.box{
  box-shadow:0 2px 6px 0 rgba(32,160,255,.3);
  background-color:#20a0ff;
}
```

还可以通过 opacify 增加，通过 transparentize 来减少透明度值，如：

```
>> opacify(rgba(125,125,125, 0.6), 0.2)
rgba(125,125,125, 0.8)

>> transparentize(green, 0.5)
rgba(0, 255, 0, 0.5)
```

 

## lighten / darken / saturate / desaturate 

lighten / darken 是基于 HSL 明度变换，这个比较适合 button 按钮的 normal 态和 hover 态变换，

saturate / desaturate 是基于 HSL 饱和度 变换，

效果可以参考这个在线工具 <http://scg.ar-ch.org/>

然而生成的颜色很丑，不实用。

 

## tint / shade

阿里的 [Ant Design](https://ant.design/docs/spec/colors-cn) 早期版本使用了 tint / shade 色彩算法，通过增加 白色（tint） 和 黑色（shade） 的占比来生成系列色。

```
.demo{
  tint( $base-color, 10% )
  shade( $base-color, 10% )
}
```

![img](https://images2017.cnblogs.com/blog/520689/201709/520689-20170919172916540-946337193.png)

 

这个在项目中会更加实用，不过要注意新生成的颜色与文本对比度需满足 WCAG 2.0 对比度要求。

在线 checker：<http://webaim.org/resources/contrastchecker/>

 

## complement 补色

在色彩理论中，如果一种颜色与另一种颜色混合后，呈现中性的灰黑色，那么这两种颜色就互为补色。

好莱坞电影比较常用补色后期手法，强烈的互补色对比，能渲染出比较冲击的视觉系氛围。如下图《天使爱美丽》海报的红绿互补。

 

![img](https://images2017.cnblogs.com/blog/520689/201709/520689-20170919173735556-1538486926.png)

不过现在还没用到这个函数，怕有点 hold 不住：）