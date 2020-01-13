# Vue

## vue基础 

vue.js的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进DOM的系统



vue中注册组件

```vue
// 定义名为 todo-item 的新组件
Vue.component('todo-item', {
  template: '<li>这是个待办项</li>'
})
```



除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 `$`，以便与用户定义的属性区分开来。例如：

```vue
var data = { a: 1 }
var vm = new Vue({  // vm是实例名
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
```







##vuex

vuex中的action可以发异步请求，也可以发同步请求

vuex中的getters中的方法名可以被组件中直接引用，且方法中不能用this来指代整个getters，必须在方法参数中添加getters这个参数，才可以调用自身的方法，完整形式： ***** （state，getters）{ }



##router

###路由传参

主要分为query和params两种方式传参

传递参数的方式：

#### 1.params

this.$router.push({

​	name：”/detail“,

​	params:{

​		code：‘100011’

​	}

})

####2.query

接收参数的方式：

query主要使用path来传参，this.$route.query.name

params要用name来引入,this.$route.params.name

```
row[k] = value[k] k 不仅可以代表下标，也可以代表对象的key值
```
```
npm i jszip -S or npm install jszip   下载jszip

 npm install three --save    下载 three.js
 
```


### 父子组件

1、第一条是否应该说成: 子组件可以使用 props 接收父组件的数据。
2、子组件可以使用 $emit 触发父组件的自定义事件。

vm.$emit( event, arg ) //触发当前实例上的事件

vm.$on( event, fn );//监听event事件后运行 fn； 

子组件

```vue

<template>
  <div class="train-city">
    <h3>父组件传给子组件的toCity:{{sendData}}</h3> 
    <br/><button @click='select(`大连`)'>点击此处将‘大连’发射给父组件</button>
  </div>
</template>
<script>
  export default {
    name:'trainCity',
    props:['sendData'], // 用来接收父组件传给子组件的数据
    methods:{
      select(val) {
        let data = {
          cityname: val
        };
        this.$emit('showCityName',data);//select事件触发后，自动触发showCityName事件
      }
    }
  }
</script>
 ———————————————— 
原文链接：https://blog.csdn.net/sllailcp/article/details/78595077
```

父组件

```vue

<template>
    <div>
        <div>父组件的toCity{{toCity}}</div>
        <train-city @showCityName="updateCity" :sendData="toCity"></train-city>
    </div>
<template>
<script>
  import TrainCity from "./train-city";
  export default {
    name:'index',
    components: {TrainCity},
    data () {
      return {
        toCity:"北京"
      }
    },
    methods:{
      updateCity(data){//触发子组件城市选择-选择城市的事件
        this.toCity = data.cityname;//改变了父组件的值
        console.log('toCity:'+this.toCity)
      }
    }
  }
</script>
```

![父子组件传值](C:\Users\wsco\Desktop\good good study，day day up\图片\父子组件传值.png)



### 路由和组件的常用两种懒加载方式：

1、**vue异步组件实现路由懒加载**

　　component：resolve=>(['需要加载的路由的地址'，resolve])

2、**es提出的import(推荐使用这种方式)**

　　**const HelloWorld = （）=>import('需要加载的模块地址')**



### v-if与v-show的区别

## v-if

条件渲染，即，使用了 v-if

- 如果满足条件，则整个子节点都会被渲染出来，包括事件的绑定等
- 如果不满足条件，则整个子节点都会被删除，包括事件也会被解绑

## v-show

实际上就是 display:none 的快捷方式。

v-show 只是隐藏了节点的显示，但是节点还在，其绑定的事件也都还在。

## v-if 和 v-show 的不同使用场景

从两者的原理可以看出，v-if 的来回切换成本很高。而 v-show 在初始化时，需要全部渲染，成本相对 v-if 要高。

所以

- 需要频繁切换状态的场景，使用 v-show
- 要加快初始化时的渲染速度，使用 v-if



## v-for

在 `v-for` 块中，我们可以访问所有父作用域的属性





## 创建一个vue项目

* 安装npm
  * npm全程为Node Package Manager， 是一个基于Node.js的包管理器，也是整个Node.js社区最流行，支持的第三方模块最多的包管理器
  * npm -v


* 由于网络原因  安装cnpm
  * npm install -g cnpm --registry=https://registry.npm.taobao.org 
* 安装vue-cli
  * cnpm install -g @vue/cli
* 安装webpack
  * cnpm install -g webpack
  * webpack 是JavaScript打包器（module bundler）




### 计算属性

是**计算属性是基于它们的响应式依赖进行缓存的**，计算属性较方法的不同之处在于，方法每次调用都要重新计算



### 计算属性和watch的区别

使用 `watch` 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的



#### 根实例特有的属性选项

```vue
new vue（{
	el： ‘’  // 特有的属性
}）

```



### input三个修饰词

```vue
.lazy 将input监听编程change监听
.number 限制输入的为数字
.trim 将用户输入的前后空白取消掉
```



### Vue的规则

父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。





###html的特性

html 语言是不区分大小写的

kebab-case 短横线命名方式  html的命名方式

camelCased 驼峰式命名方式  js的命名方式

{{ }}语法中不能是短横线连接方式。此处只能是驼峰命名方式。若为短横线的命名方式，则会报错

https://blog.csdn.net/wangxiaoxiaosen/article/details/75005949



不同于组件和 prop，事件名不存在任何自动化的大小写转换