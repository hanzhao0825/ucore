# 练习1
在信号量semaphore里面，存在一个成员value表示资源剩余量，一个waitqueue表示当前的等待队列

当一个线程请求资源的时候哦，调用down函数。如果value大于0,则获得资源并返回。如果value等于0,则将线程放入等待队列并设为睡眠状态。同时调度其他线程。

当一个资源被释放的时候，调用up函数。释放该资源。如果当前等待队列为空，则value+1,否则唤醒一个队列中的线程。

如果要增加用户态的信号量，那么必须处理好特权级的转换。我们可以新增3个系统调用sem，up和down，用来调用内核态中的上述函数。这样可以保证拥有足够的特权级来调度进程。

# 练习2
在条件变量里面，有一个成员变量value表示正在等待的线程个数，一个队列表示等待线程。有一个mutex表示进入管程的信号量，一个数组表示管理条件，一个next表示下一个线程，nextconut表示后面等待的线程数量。

线程调用cond_signal的时候，条件成立，唤醒该线程，重新开始调度。
线程调用cind_wait的时候，需要等待条件。这时让出控制权，然后释放mutex，进入睡眠。

在就餐问题中，如果在申请叉子的过程中发现叉子不够，则进入等待，条件为相邻人不在吃。释放叉子的时候，自己不在吃，然后唤醒相邻人。

对于用户态条件变量，我们还是可以写三个系统调用来进行条件变量的初始化，等待，和释放。这样可以保障特权级足够调动线程。

# 实现里没有的知识点
读者写者问题
