#### 1、BeanFactory和FactoryBean

BeanFactory：bean工厂类接口，是负责生产和管理bean的工厂，是IOC容器最底层的接口



FactoryBean：是属于Spring的一个bean，在IOC容器的基础上给bean的实现加上了一个简单工厂和装饰模式，是一个可以生产或修饰对象生成的工厂Bean，生产的对象由getObject()方法决定的；而且它是繁星的，只能固定生产某一类对象



#### 2、Spring IOC的理解，初始化过程

IOC：Inversion Of Control，即叫做”控制反转“是设计思想；也就是由IOC容器控制对象的创建和注入依赖对象（反转），为何注入依赖对象是反转？因为是容器来查找和注入依赖，对象只是被动接受，依赖对象的获取被反转了

IOC很好的体现了面向对象的设计法则之一——”别找我们，我们找你“，也就是由IOC容器帮对象找到相应的依赖对象并注入，而不是对象主动去找

> IOC容器负责实例化、定位、配置应用程序中的对象及建立这些对象间的依赖



DI：Dependency Injection，依赖注入，即由容器动态的将某个依赖关系注入到组件中

IOC容器就具有依赖注入功能



#### 3、BeanFactory和ApplicationContext

BeanFactory和Application都是IOC的实现；

ApplicationContext是BeanFactory的子类；

BeanFactory是专注于提供基础的IOC功能，ApplicationContext是为了集成更多便于开发的特性的IOC实现



1.BeanFactroy采用的是延迟加载形式来注入Bean的，即只有在使用到某个Bean时(调用getBean())，才对该Bean进行加载实例化，这样，我们就不能发现一些存在的Spring的配置问题。而ApplicationContext则相反，它是在容器启动时，一次性创建了所有的Bean。这样，在容器启动时，我们就可以发现Spring中存在的配置错误。 相对于基本的BeanFactory，ApplicationContext 唯一的不足是占用内存空间。当应用程序配置Bean较多时，程序启动较慢。

BeanFacotry延迟加载,如果Bean的某一个属性没有注入，BeanFacotry加载后，直至第一次使用调用getBean方法才会抛出异常；而ApplicationContext则在初始化自身是检验，这样有利于检查所依赖属性是否注入；所以通常情况下我们选择使用 ApplicationContext。
应用上下文则会在上下文启动后预载入所有的单实例Bean。通过预载入单实例bean ,确保当你需要的时候，你就不用等待，因为它们已经创建好了。

2.BeanFactory和ApplicationContext都支持BeanPostProcessor、BeanFactoryPostProcessor的使用，但两者之间的区别是：BeanFactory需要手动注册，而ApplicationContext则是自动注册。（Applicationcontext比 beanFactory 加入了一些更好使用的功能。而且 beanFactory 的许多功能需要通过编程实现而 Applicationcontext 可以通过配置实现。比如后处理 bean ， Applicationcontext 直接配置在配置文件即可而 beanFactory 这要在代码中显示的写出来才可以被容器识别。 ）

3.beanFactory主要是面对与 spring 框架的基础设施，面对 spring 自己。而 Applicationcontex 主要面对与 spring 使用的开发者。基本都会使用 Applicationcontex 并非 beanFactory 。



#### 4、Spring Bean的生命周期是如何被管理的





#### 5、Spring Bean的加载过程是怎样的



#### 6、如果要你实现Spring AOP，请问怎么实现





#### 7、实现Spring IOC要注意哪些问题



#### 8、Spring的事务管理机制

事务管理的本质就是封装了数据库对事务支持的操作

事务是指作为单个逻辑工作单元执行的一系列操作，特性：原子性、一致性、隔离性、持久性



> https://yun.itheima.com/course/444.html



#### 9、Spring的不同事务传播行为有哪些，做什么用的

> 事务传播行为用来描述由某一个事务传播行为修饰的方法被嵌套进另一个方法时事务如何传播

Spring中有七种事务传播行为

1. `PROPAGATION_REQUIRED`	如果当前没有事务，就新建一个事务，如果已经存在一个事务，加到这个事务中

2. `PROPAGATION_SUPPORTS`	支持当前事务，如果当前没有事务，就以非事务方式执行

3. `PROPAGATION_MANDATORY`	使用当前的事务，如果当前没有事务，就抛出异常

4. `PROPAGATION_REQUIRES_NEW`	新建事务，如果当前存在事务，把当前事务挂起

5. `PROPAGATION_NOT_SUPRORTED`	以非事务方式执行操作，如果当前存在事务，就把当前事务挂起

6. `PROPAGATION_NEVER`	以非事务方式执行，如果当前存在事务，则抛出异常

7. `PROPAGATION_NESTED`	如果当前存在事务，则在嵌套事务内执行，如果当前没有事务，则执行与`PROPAGATION_REQUIRED`类似的操作

​		  

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

// 循环依赖分两种，一种是构造器的循环依赖，另一种是属性的循环依赖



#### Spring如何解决循环依赖的？

Spring通过三级缓存来解决，一级缓存为单例池 `singletonBojects` ，二级缓存为 `earlySingletonObjects` ，三级缓存为`singletonFactories` 。当A、B两个类发送循环引用时，在A完成实例化后，就使用实例化后的对象去创建一个对象工厂，并添加到三级缓存中，如果A被AOP代理那么通过这个工厂获取到的就是A代理后的对象如果A没有被AOP代理，那么这个工厂获取到的是A实例化的对象，当A进行属性注入时，会去创建B，同时B又依赖A，所以创建B的同时会去调用 `getBean(a)` 来获取需要的依赖，，此时的`getBean(a)` 会从缓存中获取，第一步，先获取到三级缓存中的工厂，第二步，调用对象工厂的getObject方法来获取到对应的对象，得到这个对象后将其注入到B中，B会走完它的生命周期流程，当B创建完后，会将B再注入到A中，A再完成生命周期



#### 13、Spring AOP的理解





#### 14、Spring 如何保证Controller并发的安全？

1. 尽量不在Controller中定义成员变量
2. 如果要定义非静态的成员变量，则通过注解`@Scope("prototype")`，将其设置为多例模式
3. 在Controller中使用ThreadLocal保存成员变量，将成员变量保存在线程的变量域中，让不同的请求隔离开



#### Spring的自动装配

在Spring中可以把bean的依赖关系声明在配置文件中，Spring容器能够自动装配bean之间的关系

自动装配有四种模式：no、byName、byType、constructor

no选项表示自动装配为关闭状态，必须在bean定义中使用`<property`标签设置依赖项

`byName` 是基于bean名称注入依赖项；

`byType` 是基于bean类型注入依赖项；

`constructor` 是通过构造函数自动装配；

除了配置文件中提供自动装配模式外，还可以使用`@Autowired`在bean中指定自动装配，首先要启用自动注入，添加配置文件：`<context:annotation-config/>`，`<bean class ="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>`也可以启用









