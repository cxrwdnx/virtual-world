# springboot安全监控

1. 通过actuator/+端点名就可以获取相应的信息



端点名	描述
autoconfig	所有自动配置信息（ positiveMatches :运行的， negativeMatches 未运行组件）
auditevents	审计事件
beans	所有Bean的信息
configprops	所有配置属性
dump	线程状态信息
env	当前环境信息
health	应用健康状况
info	当前应用信息
metrics	应用的各项指标
mappings	应用@RequestMapping映射路径
shutdown	关闭当前应用（默认关闭）
trace	追踪信息（最新的http请求）
heapdump	下载内存快照