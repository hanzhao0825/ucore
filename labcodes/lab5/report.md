## 练习1
设置trapframe的各种成员:
cs为用户代码段
ds es ss为用户数据段
eip为代码位置，esp为stack顶端，eflags为是否允许中断

tf设置为用户态之后，返回运行的时候就到了用户态

## 练习2
按照注释编写代码，复制所需要的页，然后修改页表。

复制mm_struck的时候，直接复制vma的指针，然后设为只读。
也缺页的时候，复制对应的页，然后修改mm_struct

## 练习3
fork的时候，创建新进程，复制父进程状态，设为runnable
exec的时候，load_icode，复制新程序，执行
wait的时候，找符合条件的子进程，如果已经退出，则回收资源；如果正在运行，则变成sleeping
exit的时候，回收大部分资源，进入僵尸状态，如果父进程等待则唤醒

-----------------------------
                                            
  alloc_proc                                 RUNNING
      +                                   +--<----<--+
      +                                   + proc_run +
      V                                   +-->---->--+ 
PROC_UNINIT -- proc_init/wakeup_proc --> PROC_RUNNABLE -- try_free_pages/do_wait/do_sleep --> PROC_SLEEPING --
                                           A      +                                                           +
                                           |      +--- do_exit --> PROC_ZOMBIE                                +
                                           +                                                                  + 
                                           -----------------------wakeup_proc----------------------------------
-----------------------------
