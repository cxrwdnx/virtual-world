# Mybatis

### 注意事项

mybatis中 if的判断条件 出现installTime  != '' 这个判定

因为mybatis映射文件中data不能与string比较





### mybatis连接数据时间问题

jdbc.url=jdbc:mysql://localhost:3306/demo?serverTimezone=UTC&characterEncoding=utf-8 
jdbc.url=jdbc:mysql://localhost:3306/demo?serverTimezone=GMT%2B8&characterEncoding=utf-8 

jdbc.url=jdbc:mysql://localhost:3306/demo?serverTimezone=Asia/Shanghai&characterEncoding=utf-8 