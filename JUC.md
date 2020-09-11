JUC同步工具

> 参考：https://www.dazhuanlan.com/2020/01/29/5e30fd61e732b/

`java.util.concurrent ` 包

#### ReentrantLock

> Java提供了synchronized关键字用于加锁，但这种锁很重，且获取时必须一直等待
>
> 所以用ReetrantLock替代synchronized

需要使用try块将lock包起来，在finally块中unlock，以保证一定能解锁

可中断	`lockInterruptibly()`

可以使用 `tryLock()` 尝试锁定，返回boolean类型的值，，不管是否锁定，方法都会继续执行

可限时	 `tryLock(long timeout, TimeUnit unit)`

可设置为公平锁，默认是非公平	`ReentrantLock fairLock = new ReentrantLock(true)`

可重入 和synchronized一样

需要手动解锁 `lock.unlock()`

#### CountDownLatch	倒数计时器

允许一个或多个线程一直等待，直到一组在其他线程执行的操作全部完成

> 多个线程都达到了预期状态或完成了预期工作时，就触发事件，其他线程可以等待这个时间来触发自己后续的工作；
>
> 到达自己预期状态的线程会调用CountDownLatch的countDown()方法，表示自己已到达，而等待的线程会调用CountDownLatch的await()方法，等计数减到0，也就是都到达预期状态，触发这个等待的线程；
>
> 每次调用countDown方法时，计数会减1，直到0为止，此时调用await方法的线程被唤醒（没减到1时是阻塞状态）



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







#### CyclicBarrier	循环栅栏

一组线程会互相等待，直到所有线程都到达一个同步点，就像一群人被困到了一个栅栏前面，只有等最后一个人到达之后，他们才可以合力把栅栏（屏障）突破，可以循环使用

`public CyclicBarrier(int parties, Runnable barrierAction)`

`parties`	线程个数

`barrierAction`	计数器一次计数完成后，要执行的动作



#### Phaser 阶段



#### ReadWriteLock 读写锁

读写锁的概念其实就是共享锁与排他锁，读锁就是共享锁，写锁就是排他锁



#### Semaphore	信号量

用来控制同一时间，资源可被访问的线程数量，一般可用于流量的控制

permits成员变量是允许的线程数量

`acquire()`  阻塞方法

`release()`  线程结束之后要释放

默认是非公平锁，第二个参数设置为true是公平锁





#### LockSupport





































