# idea快捷键设置

### 虚拟机配置项

```idea
// 只有达到内存16g并且操作数为64才需要读下面的参数进行设置

-Xms128m   初始内存数
-Xmx750m   最大的内存数
-XX:ReservedCodeCacheSize=240m	 保留的代码缓存大小
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
```

