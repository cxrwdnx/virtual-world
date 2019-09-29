# IDEA

## 基础部分

### 多态

1.父类调用子类实例，引用可以调用子类重写的方法，不能调用子类独有的方法,多态也指的是方法，属性依然是调用父类的属性

````java

````





## 集合

### 注意事项

#### Arrays.asList

````java
1.运行下面的程序
List<Integer> list = Arrays.asList(1,2,3,4,5);
list.add(5);
会报错：Exception in thread "main" java.lang.UnsupportedOperationException
原因分析： 底层表示的是"数组"，因此不能调整尺寸
````

