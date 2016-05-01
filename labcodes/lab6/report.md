## 练习1

init：初始化调度队列
enqueue：将进程加入队列
dequeue：将进程移出队列
pick_next：从队列中取出一个作为下次的进程

初始化完成之后，系统用schedule来调度进程。当前进程->队列，然后条u安一个进程，出队列并运行。round robin算法中，每个时间片结束时，调用schedule，将其放到队尾，然后取队头执行

在class里维护n个队列，然后在proc_struct里面添加pos记录表示上次位于什么队列。
enqueue时push到pos的队列，
tick时re_sche=1,调用schedule，
dequeue的时候取出队列，pos+=1

## 练习2
按照注释：初始化的时候，队列头<-NULL，计数器清零。
enqueue用斜堆合并，更新time_slice和计数器
tick时候和roundrobin相同
dequeue时候用斜堆删除，计数器-=1
pick时候选队列头，stride+=BIG_STRIDE/priority


