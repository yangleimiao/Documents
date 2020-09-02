# JVM 的GC算法与10种垃圾回收器



### GC算法

#### 引用计数算法（Reference counting）

每个对象在创建时，就给这个对象绑定一个计数器，每当有一个引用指向该对象时，计数器加1，每当一个指向它的引用被删除时，计数器减1，当计数器为0时，代表没有引用指向它，这时可以对此进行垃圾回收



#### 标记-清除算法（Mark-Sweep）

为每个对象存储一个标记位，记录对象的存活状态

在标记阶段，为每个对象更新标记位，检查对象是否死亡，清除阶段，对死亡的对象进行清除

#### 标记-整理算法（Mark-Compact）

标记-整理是标记-清除的一个改进版，在标记阶段，将所有对象标记为存活或死亡，在第二阶段，将所有存活的对象整理一下放到另一处空间，然后将剩下的对象全部清除。



#### 复制算法（Copy）

将内存平均分成两部分，每次只使用一部分，当这部分内存满的时候，将内存中所有存活对象复制到另一半内存中去，将之前的一部分内存清空，如此循环下去







### 10种垃圾回收器

> 算法是垃圾回收的策略，而垃圾回收器是根据算法进行垃圾回收的具体实现



按不同年代分：

新生代收集器：Serial、ParNew、Parallel Scavenge

老年代收集器：CMS、Serial Old、Parallel Old

不分代：G1





![image-20200624102232599](/Users/yanglei/Library/Application Support/typora-user-images/image-20200624102232599.png)



#### Serial收集器

JDK1.3.1之前，Serial是HotSpot新生代收集的唯一选择；到JDK1.7为止，依然是Java虚拟机运行在Client模式下的默认收集器；

单线程收集，会发生Stop-the - world，暂停所有工作线程 然后进行垃圾回收；

在桌面应用场景中，收集新生代的几十兆内存可以控制在几十毫秒；但随着内存增大，STW时间会变长；



#### Serial Old 收集器

老年代收集器；使用Mark-Compact 标记整理算法；

也是单线程收集，发生stop-the-world，暂停所有工作线程，然后进行垃圾回收；



#### ParNew收集器

新生代收集器；并发收集器；

可以说是Serial收集器的多线程版本；也采用copy算法；

在server模式下，ParNew收集器是非常重要的收集器，因为除Serial外，目前只有它能与CMS收集器配合工作



#### Parallel Old收集器

老年代收集器；

Serial Old的多线程版本；也是标记-整理算法；会有STW；

与Parallel Scavenge 的配合是吞吐量优先的场景的选择；



#### Parallel Scavenge收集器

新生代收集器；使用复制算法；

吞吐量优先的收集器；

主要适合在后台运算而不是太多交互的任务，高吞吐量则可以最高效率的利用CPU时间,尽快的完成程序的运算任务；





#### CMS

Concurrent Mark Sweep；

并发收集器，在工作线程执行的同时可以进行垃圾回收；

分为4个过程：初始标记、并发标记、重新标记、并发清理

初始标记：标记GC Roots能直接到的对象，会有很短的Stop-The-World时间；

并发标记：进行GC Roots Tracing的过程，工作线程进行的同时，进行标记；

重新标记：为了修正并发标记期间因用户程序继续运行而导致标记产生的那一部分对象，仍然存在STW

并发清除：对标记的对象进行清除回收



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510173310943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpNjQ2NDk1OTQ2,size_16,color_FFFFFF,t_70)



> CMS是个承前启后的收集器



以下是不分代收集器

#### G1（Garbage First）

在G1中，内存空间逻辑上被分成一个个Region

采用标记整理算法，避免了CMS中出现的内存碎片问题，另外它能达到可控的垃圾回收时间；

工作过程：

初始标记：只标记GC Root关联的对象；

并发标记：分析GC Root到所有对象的可达性分析；JVM是使用Remembered Set保存了对象引用的调用信息，在可达性分析的时候只需要同时遍历remembered set就好了，不需要从根节点开始挨个遍历。

最终标记：由于并发标记阶段，用户线程还在继续工作，标记会有误差，这时需要remembered set log记录这些变化，在最终标记这个阶段将改变合并到remembered set 中，完成最终标记；

筛选清除：通过标记整理算法，根据用户配置的回收时间，和维护的优先级列表，优先收集价值最大的region，收集阶段通过标记整理和复制算法实现；



#### ZGC 

Z Garbage Collector；是一个可伸缩的、低延迟的垃圾回收器；

使用标记-整理算法；

https://www.jianshu.com/p/92fd7fdc77ac



#### Shenandoah







#### Epsilon











​	













