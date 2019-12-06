# css

### 注意事项

1.  如果页面出现白边，没有被背景图片覆盖住

   可能原因：

   一：上部图层高度/宽度超出了下部图层的高度/宽度

   二：背景图片没有随屏幕大小变化
   ​		解决方法，添加css式样：background-size: cover; 



### 知识点

###### keyframes 规则的意思 

```
{
from {top:0px;}
to {top:200px;}
}
```



### css

```
以元素起始点做大小伸缩变换
```


#### box-sizing

content-box  width，height为内容宽度

border-box    width，height包括内边距和边框宽度



```
text-indent 
```
