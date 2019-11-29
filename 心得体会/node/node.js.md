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

