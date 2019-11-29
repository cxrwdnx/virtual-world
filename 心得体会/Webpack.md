# Webpack4.0

webpack 使用采用的是node的写法

### webpack可以做的事情

1.代码转换

2.文件优化

3.代码分割

4.模块合并

5.自动刷新

6.代码校验

7.自动发布



### 学习内容

1.常见配置

2.高级配置

3.优化策略

4.ast抽象语法树

5.webpack中的Tapable

6.掌握webpack流程，手写webpack

7.手写webpack中常见的loader

8.手写webpack中常见的plugin



### webpack安装包

1.安装本地的webpack

2.webpack  webpack-cli  -D （开发依赖，生产环境不需要）



3.进入cmd

yarn init -y    初始化



4.yarn add webpack webpack-cli -D



5.npx webpack

#### webpack可以进行0配置

打包工具  -> 输出后的结构（js模块）

打包（支持js的模块化）



#### 手动配置webpack

默认配置文件的名字 wepack.config.js

指定webpack配置文件webpack --config webpack.config.my.js



#### HTML 插件

yarn add webpack-dev-sever    开发依赖，静态服务，内置express