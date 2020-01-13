###Blob

*  Blob(Binary Large Object)二进制大对象，早期数据库因为要存储声音、图片、以及可执行程序等二进制数据对象所以给该类对象取名为Blob
* **在Web领域，Blob被定义为包含只读数据的类文件对象。**Blob中的数据不一定是js原生数据形式。常见的File接口就继承自Blob，并扩展它用于支持用户系统的本地文件。



### Blob的构造器

构建一个Blob对象通常有三种方式：

1. 通过Blob对象的构造函数来构建。
2. 从已有的Blob对象调用slice接口切出一个新的Blob对象。
3. canvas API toBlob方法，把当前绘制信息转为一个Blob对象。下面只看第一种的实现：



用法：新方法创建Blob 对象（构造函数来构建）

```html
var blob = new Blob(array[optional], options[optional]);
```

构造函数，接受两个参数

第一个参数：为一个数据序列，可以是任意格式的值，例如，任意数量的字符串，Blobs 以及 ArrayBuffers。
第二个参数：用于指定将要放入Blob中的数据的类型(MIME)（后端可以通过枚举MimeType，获取对应类型：
MimeType mimeType = MimeType.toEnum(file.getContentType());）。

  <script>
    var blob = new Blob(["Hello World!"],{type:"text/plain"});
  </script>
####Blob对象的基本属性：

* size ：Blob对象包含的字节数。(只读)
* type ： Blob对象包含的数据类型MIME，如果类型未知则返回空字符串。
  Blob对象的基本方法： 

####大文件分割 (slice() 方法)，slice方法与数组的slice类似。

* Blob.slice([start, [end, [content-type]]])
  * slice() 方法接受三个参数，起始偏移量，结束偏移量，还有可选的 mime 类型。如果 mime 类型，没有设置，那么新的 Blob 对象的 mime 类型和父级一样。

当要上传大文件的时候，此方法非常有用，可以将大文件分割分段，然后各自上传，因为分割之后的 Blob 对象和原始的是独立存在的。

不过目前浏览器实现此方法还没有统一，火狐使用的是 mozSlice() ，Chrome 使用的是 webkitSlice() ，其他浏览器则正常的方式 slice() 

可以写一个兼容各浏览器的方法：

    function sliceBlob(blob, start, end, type) {
      type = type || blob.type;
      if (blob.mozSlice) {
          return blob.mozSlice(start, end, type);
      } else if (blob.webkitSlice) {
          return blob.webkitSlice(start, end type);
      } else {
          throw new Error("This doesn't work!");
      }
    }

