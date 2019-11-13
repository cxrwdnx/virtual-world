# linux

#### 操作命令

#####1.查看端口号

1、netstat -tunlp|grep 端口号

##### 2.解压

1.tar -zxvf  要解压的文件

##### 3.删除文件

1.rm -rf  强制删除文件夹及下面的子目录和文件

##### 4.移动文件夹（更换文件夹的名字）

1.mv

##### 5.创建文件夹

1.mkdir -p a/b/c   上级目录不存在则创建上级目录

##### 6. 后台运行jar项目

1. nohup java -jar demo-0.0.1-SNAPSHOT.jar > msg.log 2>&1 & --spring.profiles.active = prod



##### yum方式安装nginx

1. yum instal nginx   安装

2. yum list | grep nginx 查看安装了nginx的哪些包 

3. rpm -qa nginx  查看安装的nginx的版本

4. rpm -ql  （nginx-1.16.1-1.el7.x86_64） 查看相关参数配置文件路径

   ​	安装路径  /usr/sbin/nginx

   ​	配置文件 /etc/nginx/nginx.conf

5. 开启服务 systemctl  start nginx

6. 查看状态 systemctl status nginx

7. 关闭服务 systemctl stop nginx 

   注意事项如果直接通过nginx命令行去启动nginx，是不能通过systemctl销毁进程的，可以通过nginx -s stop，或者kill  进程id 方式结束进程

   注意： 这里指的nginx的主线程 master  process  nginx 

   ​

8. 两个linux命令 1. netstat  -antp

   ​				 2.ps   -ef | grep nginx	

   ​

   root目录下不可见？？？

   ​



##### 6.centOS非正常关机

1. 如果虚拟机因非正常关机，进入紧急模式，那么可以输入以下命令

   ```linux
   xfs_repair -v -L /dev/dm-0
   ```

   重启，进入系统



#### 查看linux系统的时间

date -R



### 安装linux系统的工具

##### virtual box

