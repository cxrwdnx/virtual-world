# Javascript

## array

1.map方法



## 函数

1.函数的调用

```
request.resolve 函数方法本身
request.resolve('./store.svg') 调用这个函数
```


### 时间

```javascript
new date().toLocaleString()
```

```javascript
1. 计算方法运行时间
    console.time('global')
    this.init(this.controlParam) // 初始化三维图像
    console.timeEnd('global')
```





### 深度拷贝

```javascript
https://blog.csdn.net/document_dom/article/details/88537629
```



### 事件

`transitionend` 事件会在 [CSS transition](https://developer.mozilla.org/en-US/docs/CSS/Using_CSS_transitions) 结束后触发. 当transition完成前移除transition时，比如移除css的[`transition-property`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-property) 属性，事件将不会被触发.如在transition完成前设置  [`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 为"`none"`，事件同样不会被触发。



## 性能优化

#### 浏览器内存分析工具

1、在开发者工具中选中Profiles,选择Take Heap Snapshot,点击Take Snapshot按钮

![浏览器内存分析工具1](C:\Users\wsco\Desktop\好好学习，天天向上\心得体会\javascript\图片\浏览器内存分析工具1.png)

2、选中生成的Heap Snapshot报表，在右边输入要查询的对象

![浏览器内存分析工具2](C:\Users\wsco\Desktop\好好学习，天天向上\心得体会\javascript\图片\浏览器内存分析工具2.png)

#### 内存释放

