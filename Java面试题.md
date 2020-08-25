# Java面试题

### Java集合22题

1. ArrayList 和 Vector 的区别。

2. 说说 ArrayList,Vector, LinkedList 的存储性能和特性。

   ArrayList是一个可改变大小的数组，当更多元素加入到ArrayList中时大小将会动态增长，本质上是一个数组；

   LinkedList是一个双链表，在添加和删除元素时具有比ArrayList更好的性能，但get、set比ArrayList弱；

   Vector和ArrayList类似，但属于强同步类；

   Vector和ArrayList在更多元素添加进来时会请求更大的空间，Vector请求其大小的双倍空间，而ArrayList每次size增长50%；

3. 快速失败 (fail-fast) 和安全失败 (fail-safe) 的区别是什么？

   fail-fast：在做系统设计时先考虑异常情况，一旦发生异常，直接停止并上报，在java中指的是集合中的错误检测机制，当多个线程对部分集合进行改变时，有可能触发fail-fast机制，这时会抛出ConcurrentModificationException

   Fail-safe：为了避免fail-fast机制，可以使用一些提供fail-safe的集合类，这样的集合容器在遍历时是先复制原有集合的内容，在拷贝的集合上进行遍历；

   

4. hashmap 的数据结构。

   就是将数组和链表组合在一起，数组寻址容易、插入删除困难，链表寻址困难、插入删除容易，常用的哈希函数就是用一种链地址法把数组和链表组合起来

5. HashMap 的工作原理是什么?

   HashMap基于hashing原理，我们通过put()和get()方法储存和获取对象，

6. Hashmap 什么时候进行扩容呢？

   当HashMap的元素个数（size）超过临界值（threshold）时就会自动扩容；

   临界值threshold=loaFactor*capacity

7. List、Map、Set 三个接口，存取元素时，各有什么特点？

   List特点：元素有放入顺序，可重复

   Set：无放入顺序，元素不可重复

8. Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢? 是用 == 还是 equals()? 它们有何区别?

   用equals()方法判断； 

   == 用来比较两个变量的值是否相等，也就是用于比较变量对应的内存中所存储的数值是否相同，要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作；

   如果一个变量指向的数据是对象类型，这时涉及两块内存，对象本身占用一块内存（堆内存），变量也占用一块内存，（例如Object obj = new Object()），变量obj是一个内存，new Object()是另一块，变量obj对应的内存中存储的是对象占用的内存的地址，对于指向对象类型的变量，如果比较两个对象是否指向同一个对象，需要用==比较；

   equals()用于比较两个独立对象的内容是否相同；

9. 两个对象值相同 (x.equals(y) == true)，但却可有不同的 hash code，这句话对不对?

10. heap 和 stack 有什么区别。

11. Java 集合类框架的基本接口有哪些？

12. HashSet 和 TreeSet 有什么区别？

    TreeSet 是二叉树实现的，TreeSet中的数据自动排好序，不允许null值；（TreeSet的底层是TreeMap的keySet()，而TreeMap是基于红黑树实现的，红黑树是一种平衡二叉查找树，任何一个节点的左右子树的高度都不会超过较矮那棵的一倍）

    HashSet的数据是无序的，可以放入一个null；两者都不能有重复值

13. HashSet 的底层实现是什么?

    HashSet底层是用HashMap存储数据的，当向HashSet添加元素的时候，首先计算元素的hashcode，然后通过扰动计算和按位与的方式计算出这个元素的存储位置，如果这个位置为空，就将元素添加进去，如果不为空，则用equals()比较元素是否相等，相等就不添加，否则就找空位添加

14. LinkedHashMap 的实现原理?

15. 为什么集合类没有实现 Cloneable 和 Serializable 接口？

16. 什么是迭代器 (Iterator)？

17. Iterator 和 ListIterator 的区别是什么？

18. 数组 (Array) 和列表 (ArrayList) 有什么区别？什么时候应该使用 Array 而不是 ArrayList？

    

19. Java 集合类框架的最佳实践有哪些？

20. Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢？是用 == 还是 equals()？它们有何区别？

21. Comparable 和 Comparator 接口是干什么的？列出它们的区别

    两者都是用来实现集合中元素的比较、排序；

    Comparable是在集合内部定义的方法实现的排序，位于java.util下；

    Comparator是集合外部实现的排序，位于java.lang下；

    Comparable是一个对象本身就已经支持自比较所需要实现的接口，

    Comparator是一个专用的比较器，当这个对象不支持自比较或自比较函数不满足要求时，可以写一个比较器完成两个对象之间比较大小；

    

22. Collection 和 Collections 的区别。

    Collection是一个集合接口，它提供了对集合对象进行基本操作的通用接口方法，Collection是list，set等的父接口；

    Collections是一个包装类，它包含各种有关集合操作的静态多态方法，不能实例化，就像一个工具类





### **JVM与调优21题**

1. Java 类加载过程？
2. 描述一下 JVM 加载 Class 文件的原理机制?
3. Java 内存分配。
4. GC 是什么? 为什么要有 GC？
5. 简述 Java 垃圾回收机制
6. 如何判断一个对象是否存活？（或者 GC 对象的判定方法）
7. 垃圾回收的优点和原理。并考虑 2 种回收机制
8. 垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？
9. Java 中会存在内存泄漏吗，请简单描述
10. 深拷贝和浅拷贝。
11. System.gc() 和 Runtime.gc() 会做什么事情？
12. finalize() 方法什么时候被调用？析构函数 (finalization) 的目的是什么？
13. 如果对象的引用被置为 null，垃圾收集器是否会立即释放对象占用的内存？
14. 什么是分布式垃圾回收（DGC）？它是如何工作的？
15. 串行（serial）收集器和吞吐量（throughput）收集器的区别是什么？
16. 在 Java 中，对象什么时候可以被垃圾回收？
17. 简述 Java 内存分配与回收策率以及 Minor GC 和 Major GC。
18. JVM 的永久代中会发生垃圾回收么？
19. Java 中垃圾收集的方法有哪些？
20. 什么是类加载器，类加载器有哪些？
21. 类加载器双亲委派模型机制？





### 并发编程28题

1. Synchronized 用过吗，其原理是什么？
2. 你刚才提到获取对象的锁，这个“锁”到底是什么？如何确定对象的锁？
3. 什么是可重入性，为什么说 Synchronized 是可重入锁？
4. JVM 对 Java 的原生锁做了哪些优化？48
5. 为什么说 Synchronized 是非公平锁？49
6. 什么是锁消除和锁粗化？49
7. 为什么说 Synchronized 是一个悲观锁？乐观锁的实现原理又是什么？什么是 CAS，它有什么特性？
8. 乐观锁一定就是好的吗？
9. 跟 Synchronized 相比，可重入锁 ReentrantLock 其实现原理有什么不同？
10. 那么请谈谈 AQS 框架是怎么回事儿？
11. 请尽可能详尽地对比下 Synchronized 和 ReentrantLock 的异同。
12. ReentrantLock 是如何实现可重入性的？
13. 除了 ReetrantLock，你还接触过 JUC 中的哪些并发工具？
14. 请谈谈 ReadWriteLock 和 StampedLock。
15. 如何让 Java 的线程彼此同步？你了解过哪些同步器？请分别介绍下。
16. CyclicBarrier 和 CountDownLatch 看起来很相似，请对比下呢？
17. Java 线程池相关问题
18. Java 中的线程池是如何实现的？
19. 创建线程池的几个核心构造参数？
20. 线程池中的线程是怎么创建的？是一开始就随着线程池的启动创建好的吗？
21. 既然提到可以通过配置不同参数创建出不同的线程池，那么 Java 中默认实现好的线程池又有哪些呢？请比较它们的异同
22. 如何在 Java 线程池中提交线程？
23. 什么是 Java 的内存模型，Java 中各个线程是怎么彼此看到对方的变量的？
24. 请谈谈 volatile 有什么特点，为什么它能保证变量对所有线程的可见性？
25. 既然 volatile 能够保证线程间的变量可见性，是不是就意味着基于 volatile 变量的运算就是并发安全的？
26. 请对比下 volatile 对比 Synchronized 的异同。
27. 请谈谈 ThreadLocal 是怎么解决并发安全的？
28. 很多人都说要慎用 ThreadLocal，谈谈你的理解，使用 ThreadLocal 需要注意些什么？

### spring 25题

- 1、什么是 Spring 框架？Spring 框架有哪些主要模块？
- 2、使用 Spring 框架能带来哪些好处？
- 3、什么是控制反转(IOC)？什么是依赖注入？
- 4、请解释下 Spring 框架中的 IoC？
- 5、BeanFactory 和 ApplicationContext 有什么区别？
- 6、Spring 有几种配置方式？
- 7、如何用基于 XML 配置的方式配置 Spring？
- 8、如何用基于 Java 配置的方式配置 Spring？
- 9、怎样用注解的方式配置 Spring？
- 10、请解释 Spring Bean 的生命周期？
- 11、Spring Bean 的作用域之间有什么区别？
- 12、什么是 Spring inner beans？
- 13、Spring 框架中的单例 Beans 是线程安全的么？
- 14、请举例说明如何在 Spring 中注入一个 Java Collection？
- 15、如何向 Spring Bean 中注入一个 Java.util.Properties？
- 16、请解释 Spring Bean 的自动装配？
- 17、请解释自动装配模式的区别？
- 18、如何开启基于注解的自动装配？
- 19、请举例解释@Required 注解？
- 20、请举例解释@Autowired 注解？
- 21、请举例说明@Qualifier 注解？
- 22、构造方法注入和设值注入有什么区别？
- 23、Spring 框架中有哪些不同类型的事件？
- 24、FileSystemResource 和 ClassPathResource 有何区别？
- 25、Spring 框架中都用到了哪些设计模式？



### 设计模式 10题

- 1.请列举出在 JDK 中几个常用的设计模式？
- 2.什么是设计模式？你是否在你的代码里面使用过任何设计模式？
- 3.Java 中什么叫单例设计模式？请用 Java 写出线程安全的单例模式
- 4.在 Java 中，什么叫观察者设计模式（observer design pattern）？
- 5.使用工厂模式最主要的好处是什么？在哪里使用？
- 6.举一个用 Java 实现的装饰模式(decorator design pattern)？它是作用于对象层次还是类
- 层次？
- 7.在 Java 中，为什么不允许从静态方法中访问非静态变量？
- 8.设计一个 ATM 机，请说出你的设计思路？
- 9.在 Java 中，什么时候用重载，什么时候用重写？
- 10.举例说明什么情况下会更倾向于使用抽象类而不是接口



### springboot 22题

1. 什么是 Spring Boot？
2. Spring Boot 有哪些优点？
3. 什么是 JavaConfig？
4. 如何重新加载 Spring Boot 上的更改，而无需重新启动服务器？
5. Spring Boot 中的监视器是什么？
6. 如何在 Spring Boot 中禁用 Actuator 端点安全性？
7. 如何在自定义端口上运行 Spring Boot 应用程序？
8. 什么是 YAML？
9. 如何实现 Spring Boot 应用程序的安全性？
10. 如何集成 Spring Boot 和 ActiveMQ？
11. 如何使用 Spring Boot 实现分页和排序？
12. 什么是 Swagger？你用 Spring Boot 实现了它吗？
13. 什么是 Spring Profiles？
14. 什么是 Spring Batch？
15. 什么是 FreeMarker 模板？
16. 如何使用 Spring Boot 实现异常处理？
17. 您使用了哪些 starter maven 依赖项？
18. 什么是 CSRF 攻击？
19. 什么是 WebSockets？
20. 什么是 AOP？
21. 什么是 Apache Kafka？
22. 我们如何监视所有 Spring Boot 微服务？



### Netty10题

1. BIO、NIO和AIO的区别？
2. NIO的组成？
3. Netty的特点？
4. Netty的线程模型？
5. TCP 粘包/拆包的原因及解决方法？
6. 了解哪几种序列化协议？
7. 如何选择序列化协议？
8. Netty的零拷贝实现？
9. Netty的高性能表现在哪些方面？
10. NIOEventLoopGroup源码？



### Redis 16题

1. 什么是redis?
2. Reids的特点
3. Redis支持的数据类型
4. Redis是单进程单线程的
5. 虚拟内存
6. Redis锁
7. 读写分离模型
8. 数据分片模型
9. Redis的回收策略
10. 使用Redis有哪些好处？
11. redis相比memcached有哪些优势？4
12. redis常见性能问题和解决方案
13. MySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据245
14. Memcache与Redis的区别都有哪些？
15. Redis 常见的性能问题都有哪些？如何解决？
16. Redis 最适合的场景









