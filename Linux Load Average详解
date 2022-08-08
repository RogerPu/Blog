# Linux Load Average详解

#### 引言

Linux系统中的load average是SRE工程师经常关注的指标，也是SRE工程师在面试时候经常会被问到的问题，大家用它来判断`CPU`的工作负载，一般这个值如果是CPU核心数的多倍时，我们就认为CPU负载很高，需要处理，这样的认识对吗？

结论：`不完全对`。load average不仅体现CPU负载，磁盘I/O，内存不足都会造成该值上升。

#### 分析

- load average的使用场景

![](https://ask.qcloudimg.com/http-save/1076462/yjlvwr4jt8.jpeg)

![](https://ask.qcloudimg.com/http-save/1076462/cst6ixfb13.jpeg)

![](https://ask.qcloudimg.com/http-save/1076462/r6xsmhi8do.jpeg)

- 源码解读

![](https://ask.qcloudimg.com/http-save/1076462/fgwsdvi385.jpeg)

该数据来源是计算CPU的内核态线程量（等价用户态进程量）_（这里是我自己综合看各路资料总结，待确认）_，`不仅包括了nr_running状态，还包括了nr_uninterruptible状态的线程，后者是会被I/O、内存资源关联影响的。`

- 什么是nr\_running、nr\_uninterruptible状态？
这是用户态进程状态，有7种状态。running的状态好理解，就是正常运行的进程；而uninterruptible是一种特殊状态，表示的是一个等待硬件资源睡眠且无法被中断的进程，出现该状态的进程一般是因为在等待IO，例如磁盘IO、网络IO等。`也就是说，I/O和内存的不足，也会造成load average增加。`

#### 待办

- nr\_running、nr\_uninterruptible的来源测试分析。
- 内核态线程和用户态进程线程概念的理解。
- 一套测试验证方法

#### 参考材料

[https://zhuanlan.zhihu.com/p/75975041](https://zhuanlan.zhihu.com/p/75975041) | Linux Load Averages：什么是平均负载？[https://github.com/torvalds/linux/blob/master/kernel/sched/loadavg.c](https://github.com/torvalds/linux/blob/master/kernel/sched/loadavg.c) | Linux相关内核源码[https://cloud.tencent.com/developer/article/1087424](https://cloud.tencent.com/developer/article/1087424) | linuxload average详细分析

[http://www.brendangregg.com/blog/2017-08-08/linux-load-averages.html](http://www.brendangregg.com/blog/2017-08-08/linux-load-averages.html) | Linux Load Averages: Solving the Mystery

[https://blog.csdn.net/dog250/article/details/107792805](https://blog.csdn.net/dog250/article/details/107792805) | Linux系统load average异常值处理的trick
