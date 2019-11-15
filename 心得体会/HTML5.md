# HTML5

### Canvas

**canvas绘制的是位图**
这是一个所有了解过canvas的人都应该知道的知识点，也是接下来我们将要分析问题的核心。
关于位图的解释我们放在后面，现在我们只要知道canvas绘制的图像是位图。

**canvas的width和height属性**
canvas的width和height属性是初学者非常容易搞错的内容。这两个属性经常会与css中的width和height属性混淆。
比如我们有如下代码（1）:

```html
<canvas width="600" height="300" style="width: 300px; height: 150px"></canvas>
```

- style中的width和height分别代表canvas这个元素在界面上所占据的宽高，即样式上的宽高
- attribute中的width和height则代表canvas实际像素的宽高




### 模糊原因的初步探讨

上面是对所需基础知识的一些简介，下面开始正式进行探究。

首先我们提到使用canvas绘制图像的是位图，而我们平常用的jpg，png也是位图。那么什么是位图？

位图又叫像素图或栅格图，它是通过记录图像中每一个点的颜色、深度等信息来存储和显示图像。具象一点讲，可以将位图想象成一个巨大的拼图，这个拼图有无数的拼块，每个拼块代表了一个纯色的像素点。**理论上，1个位图像素对应着1个物理像素**。但假如说你使用了高清屏，比如苹果的retina屏去查看一幅图画，又会是什么样子呢？

假设我们有如下代码，该代码将展示在iphone4的retina屏上：

```html
<canvas width="320" height="150" style="width: 320px; height: 150px"></canvas>
```

iphone4本身的物理像素为640 *980，而设备独立像素为320 *480，这代表着1个css像素实际由4个物理像素构成，canvas的像素为320 *150，其css像素为320 *150，则代表1个css像素将会由1个canvas元素构成，这样进行换算，**在retina屏幕下，1个canvas像素（或者说是1个位图像素）将会填充4个物理像素，由于单个位图像素不可以再进一步分割，所以只能就近取色，从而导致图片模糊。**

如果还有疑惑的话，以下的图片可以说明位图在retina屏幕下是如何填充的：

![5cc53525e3647](C:\Users\wsco\Desktop\好好学习，天天向上\图片\心得体会\5cc53525e3647.jpg)

上图中左侧的是在普通屏幕下的显示规则，可以看出有4个位图像素点，而右侧的高清屏幕下则有16个像素点。由于像素点不可切割的原因，颜色产生了改变。

但是还有一点没有解释清楚，就是为什么图片会就近取色而不是直接取原值，这也是导致模糊的幕后黑手。



### 幕后黑手---平滑处理技术

下面是我的某位大佬同学帮我解释的，刚才我们说了每个位图元素实际上一个纯色的像素点。现在假设我们需要在一个css大小为4px * 4px，dpr为1普通屏幕上绘制一个数字“0”，那么我们绘制的样子应该如下图，其中1代表黑色像素点，0代表白色像素点。

![5cc5352cbbb75](C:\Users\wsco\Desktop\好好学习，天天向上\图片\心得体会\5cc5352cbbb75.jpg)

可以看出在dpr比较小的情况下，我们的“0”这个图案还比较明显，现在假如我们css大小不变，但是改成在retina屏幕下绘制图像，效果又会变成什么样呢？

![5cc53534502e4](C:\Users\wsco\Desktop\好好学习，天天向上\图片\心得体会\5cc53534502e4.jpg)

我们已知在retina屏幕下，一个css像素代表4个物理像素，假如我们不做任何处理，直接按照上面矩阵排列，将矩阵扩大的话，会发现在retina屏幕下，我们的图案锯齿感非常明显，图像明显缺乏了一丝顺化。

假如我们对图像稍作改变，改成下图这样

![5cc5353aec4c4](C:\Users\wsco\Desktop\好好学习，天天向上\图片\心得体会\5cc5353aec4c4.jpg)

图像感觉瞬间柔和了，**但是原本应该4个0充斥的地方变成了3个1加上1个0。这其实就是所谓的图像平滑处理，为了解决锯齿感觉，将原本的颜色改变，在充斥着较多颜色的图片上，为了更自然，图片的连接处变成了近似的颜色，这也解释了为什么上面填充颜色的时候不是使用本色而是使用近似色。**



### 原因总结

通过了上述的解释，现在我们来总结以下结论，在移动端盛行，高清屏基本上已经普及的现在，1px的css像素实际上代表了4个甚至更多的物理像素。但是由于我们的代码问题，我们1px的css像素和1个canvas像素画上了等号，也就导致了1个canvas像素实际需要填充4个甚至更多物理像素，为了保证图像平滑处理，在填充剩余的物理像素时采用了原先颜色的近似值，导致了图像的模糊。



### 解决思路

了解了问题出现的原因，解决问题就很容易，解决该问题最重要的一点是让1个canvas像素和一个物理像素挂等号

**高版本的浏览器的window对象下都挂着一个devicePixelRatio属性，该属性就是上面所说的dpr,**

在canvas元素css宽高确定的情况下，我们可以这么做

```javascript
let canvas = document.getElementById('canvas');
let ctx = canvas.getContext('2d');
let dpr = window.devicePixelRatio; // 假设dpr为2
// 获取css的宽高
let { width: cssWidth, height: cssHeight } = canvas.getBoundingClientRect();
// 根据dpr，扩大canvas画布的像素，使1个canvas像素和1个物理像素相等
canvas.width = dpr * cssWidth;
canvas.height = dpr * cssHeight;
// 由于画布扩大，canvas的坐标系也跟着扩大，如果按照原先的坐标系绘图内容会缩小
// 所以需要将绘制比例放大
ctx.scale(dpr,dpr);
```



###清空canvas中的内容

\1. 最简单的方法：由于canvas每当高度或宽度被重设时，画布内容就会被清空，因此可以用以下方法清空：

```

function clearCanvas(){
    var c=document.getElementById("myCanvas");
    var cxt=c.getContext("2d");
    c.height=c.height;
}
```

2. 使用clearRect方法：

	function clearCanvas() {
	var c=document.getElementById("myCanvas");
	var cxt=c.getContext("2d");
	cxt.clearRect(0,0,c.width,c.height);
	}

