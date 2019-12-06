# Node.js

安装淘宝npm镜像

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```


#### path

1.resolve

```
var path = require("path")     //引入node的path模块

path.resolve('/foo/bar', './baz')   // returns '/foo/bar/baz'
path.resolve('/foo/bar', 'baz')   // returns '/foo/bar/baz'
path.resolve('/foo/bar', '/baz')   // returns '/baz'
path.resolve('/foo/bar', '../baz')   // returns '/foo/baz'
path.resolve('home','/foo/bar', '../baz')   // returns '/foo/baz'
path.resolve('home','./foo/bar', '../baz')   // returns '/home/foo/baz'
path.resolve('home','foo/bar', '../baz')   // returns '/home/foo/baz'

从后向前，若字符以 / 开头，不会拼接到前面的路径(因为拼接到此已经是一个绝对路径)；若以 ../ 开头，拼接前面的路径，且不含最后一节路径；若以 ./ 开头 或者没有符号 则拼接前面路径；
```



2.join

```node.js

const path = require('path');
let myPath = path.join(__dirname,'/img/so');
let myPath2 = path.join(__dirname,'./img/so');
let myPath3=path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
 
 
console.log(__dirname);           
console.log(myPath);    
console.log(myPath2);   
console.log(myPath3);  

E:\test
E:\test\img\so
E:\test\img\so
\foo\bar\baz\asdf

console.log(path.join('/img/books', '../net'))  // returns /img/net
```



##### 读写文件

```javascript
var fs = require('fs')
// 第一个参数： 文件路径   第二个参数： 文件内容   第三个参数： 回调函数
// 成功： 文件写入成功  error是 null
// 失败：文件写入失败  error就是错误对象
fs.writeFile('./data/你好.md', 'hello world')， function（error）{
}）

// 成功： data：数据      error： null
// 失败： data：undefined 没有数据， error 错误对象
fs.readFile('./data/a.txt', function(error, data) {})
```



#####http模块

```javascript
// 1. 加载http核心模块
var http = require('http')
// 2.使用http.createServer() 方法创建一个Web服务器
// 返回一个Server实例
var server = http.createServer()
// 3. 服务器要干嘛
// 提供服务： 对 数据的服务
// 发请求  接收请求  处理请求  给个反馈（返回响应）
// 注册request请求时间  当客户端请求过来， 就会自动触发服务器的request请求事件，然后执行第二个参数;回调处理
// request 请求对象
// response 响应对象
server.on('request', function (request， response) {
  console.log（'收到客户端的请求了'）
  // request.url  请求路径
  // response
})

// 4. 绑定端口号，启动服务器
server.listen(3000, function() {
  console.log('服务器启动成功了')
})

```



#### Node.js核心模块

```node
Node为JavaScript提供了很多服务器级别的API， 这些API绝大多数都被包装到了一个具名的核心模块中

文件操作的fs核心模块， http服务构建的http模块，path路径操作模块， os操作系统信息模块


```



#### 模块系统

```node
基础：
	所有联网的程序都需要进行网络通信
	
计算机中只有一个物理网卡，而且一个局域网中，网卡的地址必须是唯一的。 网卡是通过唯一的ip地址进行定位的

ip地址用来定位计算机，端口号用来定位具体的应用程序

端口号的范围是0-65535

在计算机中有一些默认端口号，最好不要去使用
	例如： http服务的80
	

http协议
// 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析
// 中文此操作系统的编码方式 GBK
// text/plain 普通文本
// text/html html格式的文本
// image/jpeg 图片不需要编码方式， 一般只有字符数据才需要指定编码方式
// url: 统一资源定位符   一个url 最终其实是需要对应到一个资源的
res.setHeader('Content-Type','text/plain ;charset=utf-8')
```

