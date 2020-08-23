#### 1、BeanFactory和FactoryBean



BeanFactory：生产和管理bean的工厂



FactoryBean：是一个能生产或修饰对象生成的工厂Bean



#### 2、Spring IOC的理解，初始化过程

IOC：Inversion Of Control，即叫做”控制反转“是设计思想；也就是由IOC容器控制对象的创建和注入依赖对象（反转），为何注入依赖对象是反转？因为是容器来查找和注入依赖，对象只是被动接受，依赖对象的获取被反转了

IOC很好的体现了面向对象的设计法则之一——”别找我们，我们找你“，也就是由IOC容器帮对象找到相应的依赖对象并注入，而不是对象主动去找

> IOC容器负责实例化、定位、配置应用程序中的对象及建立这些对象间的依赖



DI：Dependency Injection，依赖注入，即由容器动态的将某个依赖关系注入到组件中

IOC容器就具有依赖注入功能



#### 3、BeanFactory和ApplicationContext





#### 4、Spring Bean的生命周期是如何被管理的





#### 5、Spring Bean的加载过程是怎样的



#### 6、如果要你实现Spring AOP，请问怎么实现





#### 7、实现Spring IOC要注意哪些问题



#### 8、Spring的事务管理机制





#### 9、Spring的不同事务传播行为有哪些，做什么用的





#### 10、Spring中用到了哪些设计模式

单例模式：BeanFactory



适配器模式：Spring AOP的增强或通知（Advice）使用了适配器模式

工厂模式：Spring使用工厂模式通过BeanFactory、ApplicationContext创建bean对象

代理模式：Spring AOP

模板方法：jdbcTemplate、hibernateTemplate等对数据库操作的类

观察者模式：Spring 事件驱动模型

装饰者模式：





#### 11、Spring MVC的工作原理





#### 12、Spring循环注入的原理

循环依赖分两种，一种是构造器的循环依赖，另一种是属性的循环依赖





#### 13、Spring AOP的理解





#### 14、Spring 如何保证Controller并发的安全？

1. 尽量不在Controller中定义成员变量
2. 如果要定义非静态的成员变量，则通过注解`@Scope("prototype")`，将其设置为多例模式
3. 在Controller中使用ThreadLocal保存成员变量，将成员变量保存在线程的变量域中，让不同的请求隔离开























































