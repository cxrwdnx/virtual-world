# Vue

## vue基础 



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
版权声明：本文为CSDN博主「darkblueLove」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
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



