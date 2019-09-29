# 微服务

## 微服务的优缺点

### 优点

1.每个服务足够内聚，足够小，代码容易理解，这样能聚焦于一个指定的业务功能和业务需求

2.开发简单，开发效率提高，一个服务可能就是专一的只干一件事

3.微服务是能够被小团队单独开发，这个小团队是2到5人的开发人员组成

4.微服务是耦合的，是有功能意义的服务，无论是在开发阶段或者部署阶段都是独立的

5.微服务能使用不同的语言开发

6.易于和第三方集成，微服务允许容易且灵活的方式集成自动部署，通过集成工具jenkins

7.微服务易于被一个开发人员理解，修改和维护，这样小团队能够更关注自己的工作成果，无需通过合作才能体现价值

8.微服务允许你利用融合最新技术

**9.微服务只是业务逻辑的代码，不会和HTML,CSS和其他界面组件混合**

10.每个微服务可以有自己独立的数据库，也可以有统一的数据库



### 缺点

1.开发人员要处理分布式系统的复杂性

2.多服务运维难度，随着服务的增加，运维的压力也在增大

3.系统部署依赖

4.服务间通信成本

5.数据一致性

6.系统集成测试

7.性能监控



## 微服务技术栈

服务开放											springboot、spring、springmvc

服务配置与管理									Netflix公司的Archaius、阿里的Diamond等

服务注册与发现									Eureka、Consul、Zookeeeper

服务调用											Rest、Rpc、gRpc等

服务熔断器										Hystrix、 Envoy

负载均衡											Ribbon、Nginx等

服务接口调用（客户端调用服务的简化工具）			Feign

消息队列											。。。

服务配置中心管理									SpringCloudConfig、Chef等

服务路由（api网关）								Zuul

服务监控											Zabbix、Nagios、Metrics、Spectator

全链路追踪										Zipkin、Brave、Dapper

服务部署											Docker、OpenStack、Kubernetes

数据流操作开发包									SpringCloud Stream（封装与Redis，											Rabbit、Kafka等发送接收消息）

时间消息总线										Spring Cloud Bus



### SpringCloud的概念

SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务整合并管理起来，为各个微服务之间提供，配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务 

![dubbo-springCloud](C:\Users\wsco\Desktop\good good study，day day up\image\SpringCloud\dubbo-springCloud.jpg)





重要事情说三遍，mysql server8及以上url末尾应加上?serverTimezone=GMT%2B8