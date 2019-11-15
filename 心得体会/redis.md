# redis

### 1.redis在linux的相关操作

在docker中做端口映射

```linux
docker run -p 6379:6379 -v $PWD/data:/data  -d redis:3.2 redis-server --appendonly yes		
```

##### 参数说明

**-p 6379:6379 :** 将容器的6379端口映射到主机的6379端口

**redis-server --appendonly yes :** 在容器执行redis-server启动命令，并打开redis持久化配置



redis客户端连接命令：docker exec -it 0b63b7eacc29 redis-cli 启动时使用container id进行启动0b63b7eacc29