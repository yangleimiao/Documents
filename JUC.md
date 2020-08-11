JUC同步工具

> 参考：https://www.dazhuanlan.com/2020/01/29/5e30fd61e732b/

`java.util.concurrent ` 包

ReentrantLock

可中断	`lockInterruptibly()`

可限时	`tryLock()`  `tryLock(long timeout, TimeUnit unit)`

可设置为公平锁，默认是非公平	`ReentrantLock fairLock = new ReentrantLock(true)`

可重入

ReadWriteLock

Semaphore	信号量

用来控制同一时间，资源可被访问的线程数量，一般可用于流量的控制

CountDownLatch	倒数计时器

允许一个或多个线程一直等待，直到一组在其他线程执行的操作全部让暗沉

常用的方法

```java
public void await() throws InterruptedException {
	sync.acquireSharedInterruptibly(1);
}

public void countDown() {
	sync.releaseShared(1);
}
```

当一个线程调用await方法时，就会阻塞当前线程。每当有线程调用一次 countDown 方法时，计数就会减 1。当 count 的值等于 0 的时候，被阻塞的线程才会继续运行







CyclicBarrier	循环栅栏

一组线程会互相等待，直到所有线程都到达一个同步点，就像一群人被困到了一个栅栏前面，只有等最后一个人到达之后，他们才可以合力把栅栏（屏障）突破

`public CyclicBarrier(int parties, Runnable barrierAction)`

`parties`	线程个数

`barrierAction`	计数器一次计数完成后，要执行的动作

LockSupport



































