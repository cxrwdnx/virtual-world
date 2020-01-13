# Spring 单例模式和多例模式

1.Spring中的对象默认都是 单例模式。

2.使用 @Scope("prototype") 注解来使对象成为多例模式。

3.通过@Autowired 注入的Service 或者是其他实例其实是单例的。

4.通过 ApplicationContext.getBean(C.class); 获取的实例是多例的。

 

 

 

总结：在存在并发的时候，每个需要被注入的类、对象 都使用@Scope("prototype") 注解成为多例，

　　　每个需要被获取的对象通过ApplicationContext.getBean(C.class);来获取，确保每个线程获取的对象都是新的。

