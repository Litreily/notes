# 进程调度

> Linux Kernel Development ch4: Process Scheduling

多任务操作系统的进程调度分为非抢占式调度和抢占式调度，现代操作系统基本上都采用了抢占式调度。

## Linux 进程调度

1. 2.4 kernel 调度器: 设计简单、粗糙，易于理解，但是难以胜任过多可执行进程
2. 2.5 kerenl 调度器：大型改造，O(1)调度器，算法优化
3. 2.6 kernel 调度器：针对交互进程，吸取队列理论，设计RSDL调度，后更新为Completely Fair Scheduler(CFS)

## 策略

`Policy`决定调度程序何时让什么进程运行。

### I/O 消耗型和处理器消耗型进程

- I/O 消耗型：大量的I/O请求，大部分时间在阻塞态等待I/O数据
- 处理器消耗型：大部分时间在执行代码，基本不阻塞去等待I/O，比如ssh keygen和MATLAB

进程可能同时包含以上两种行为。调度器策略需要尝试满足两种冲突需求：快速的进程响应和最大化系统利用率。为了实现这个目标，调度器使用了非常复杂的算法去决定最值得执行的进程。

Unix系统偏向于I/O消耗型进程，可以提供好的进程响应时间。Linux为了提供好的交互响应和桌面性能，优化了进程响应，更倾向于有优先调度I/O消耗型进程。


### 进程优先级

Linux采用两种优先级策略，nice值和实时优先级。

1. nice值：`-20 ~ 19`, nice值越小，优先级越高。 Linux系统使用`ps -el`，`NI`列对应的就是nice值，它代表时间片的比例。
2. 实时优先级：`0 ~ 90`, 与nice值相反，数值越高优先级越高。其值可配。查看实时进程的方式如下(rtprio)

```bash
ps -eo state,uid,pid,ppid,rtprio,time,comm
```

输出结果中`rtprio`为`-`代表不是实时进程。

!!! note
    1. 实时进程优先级高于普通进程
    2. Linux的实时优先级与nice优先级互不相交

### 时间片

调度器必须指定一个默认的时间片，但这并不简单。如果时间片过长，会导致系统交互性能变差，就感觉应用程序不是并发执行的。如果时间片过短，就会导致处理器浪费大量时间进行进程切换。同时I/O消耗型和处理器消耗型的矛盾也会显现，I/O消耗型的进程无需长的时间片，处理器消耗型的进程则相反。

较长时间片会导致系统性能低下，因此大多数操作系统的时间片都较短，比如10ms。Linux使用CFS调度器，不直接分配时间片给进程，而是将处理器使用比例分配给进程。在Linux中，进程处理时间由系统负载决定。此外，处理比例还与nice值有关系，nice值越高，处理器比例越低，反之亦然。

Linux系统是抢占式的，当一个进程进入可运行态，CFS调度器会根据分配给进程的处理比例去决定什么时候将其投入运行。如果比例低，则立即执行，抢占当前进程。否则延迟执行。

## 进程调度算法

### 调度器类

Linux调度器是模块化的，针对不同类型的进程，可以使用不同算法进行调度。这种模块化被称之为 **调度器类** (scheduler classes).调度器类允许不同的、可动态添加的调度方法去调度它们能够处理的进程。每个调度器类都有一个优先级。基本调度代码位于`kernel/sched.c`, 它会按照优先级顺序遍历调度类，拥有最高优先级的调度器类生出，并选择下面要执行的程序。

完全公平调度Completely Fair Scheduler(CFS)是用于常用进程的调度器类，在Linux系统中为`SCHED_NORMAL`, 位于`kernel/sched_fair.c`.

### Unix 系统中的进程调度

在UNIX系统中，优先级以nice值的方式输出到用户空间，这虽然看起来简单，但实际涉及很多反常问题。

首先，映射nice值到时间片需要确定每个nice值对应分配具体多大的时间片？假设有两个进程，一个是默认优先级(nice=0), 另一个是最低优先级(nice=20), 同时假设每个时间片最小单位为5ms. 那么两个进程的时间片分配如下：

| nice                 | timeslices | frequency |
| -------------------- | ---------- | --------- |
| 0 (default)          | 100ms      | 100 / 105 |
| 20 (lowest priority) | 5ms        | 5 / 105   |

如果有两个同等优先级(nice=20)的进程呢？按照上面的分配方式，每个进程都将获得5ms的时间片，然后每隔5ms切换一次，两个进程确实获得了50%的处理时间，但是切换过于频繁，大大浪费了CPU资源。以此类推，如果是两个普通进程，优先级nice=0, 它们同样可以获得50%的处理器时间，但是以100ms为增量。显然这种分配方式是不理想的，对于优先级不同的进程，虽然时间占比是合理的，但是实际的处理时间却是不理想的。

而且，通常高nice值(低优先级)的进程是后台进程，是计算密集型，需要连续执行较长时间，按照以上方式却将分得很少的时间片；而普通优先级进程多是前台用户任务，大多是I/O消耗型，大部分时间处于阻塞状态，按照以上方式却将获得更多的时间片。由此来看，以上分配方式是不合理的。

接下来看另外一个问题，同样是nice值相关的。

| nice | timeslices |
| ---- | ---------- |
| 0    | 100ms      |
| 1    | 95ms       |
| 18   | 10ms       |
| 19   | 5ms        |

nice值为0, 1的两个进程，时间片差5ms，但直观上看相差无几；但是nice值为18, 19的两个进程，时间片同样相差5ms，但却是相差两倍的处理器时间。由于nice值通常使用相对值（系统调用接受一个增量，而不是绝对值），这意味着“把进程的nice值减1”带来的影响很大程度取决于它的初始nice值。

第三个问题，如果需要映射nice值到时间片，就需要设定一个绝对的时间片。并且这个绝对值必须是内核可测量的。在大部分操作系统中，这意味着时间片必须是定时器节拍(timer tick)的整数倍。但这会引发几个问题，第一，最小时间片必须是定时器节拍的整数倍，可能是10ms，也可能是1ms；第二，系统定时器限制了时间片的差异：连续的nice值映射到时间片，差别多至10ms或者少则1ms；最后，时间片还随着定时器节拍不同而改变。

第四个问题，基于优先级的调度器可能为了优化交互任务而唤醒相关进程，这种系统中，可能为了进程能更快的投入运行，而去提升要唤醒的进程的优先级，即便它们的时间片已经耗尽。这样虽然可以提升交互性能，但也有可能给某些特殊的睡眠用例开了后门，打破了公平原则，获取更多处理器时间，损害了其它进程的利益。

上面的绝大多数问题通过改造Unix调度器都可以解决，比如将nice值呈几何增加而不是算数增加，这样可以解决上面第二个问题；使用新的度量机制将nice值到时间片的映射与定时器节拍分离，以解决第三个问题。但这些都没有解决实质问题—— **分配绝对的时间片引发的固定切换频率** ，给公平性造成很大变数。而CFS采用的方法是对时间片分配方式进行根本性的重新设计，完全摒弃时间片，并分配给进程一个 **处理器使用比重** (proportion of the processor), 通过这种方式，CFS实现了完全公平调度，并将切换频率置于不断变换当中。

### 公平调度

CFS 基于一个简单的概念：进程调度的效果表现得这个系统有一个理想、完美的多任务处理器。在这样一个系统中，每个进程将获得 $1/n$ 的处理器时间，`n` 代表可运行的进程数，我们可以调度给它们无限小的时间周期，所以在任何可测量周期内，我们给了n个进程中每个进程同样多的运行时间。

举例说明，原本的UNIX系统中，假设一个进程运行5ms后另一个进程再运行5ms，每个进程在运行时占用100%的处理器。而在一个理想完美的多任务处理器中，我们可以保证10ms内同时运行两个进程，每个占用 $50\%$ 的处理器能力。

当然，这种理想模型是不现实的，我们无法在一个处理器上真的同时运行多个进程。而且每个进程运行无限小的时间周期也是低效的，因为每次进程抢占都需要付出代价。

那么CFS是怎么做的呢？CFS允许每个进程运行一段时间、循环轮转、选择运行最少的进程作为下一个运行进程，不再采用分配每个进程时间片的做法，CFS在所有可运行进程总数基础上计算出一个进程应该运行多久，而不是依赖nice值计算时间片。nice值在CFS中被作为进程获得处理器运行比的权重，nice值越大权重越低，反之亦然。

nice值对应的权重可以参考`kernel/sched/sched.h`中的`prio_to_weight`.

```c
/*
 * Nice levels are multiplicative, with a gentle 10% change for every
 * nice level changed. I.e. when a CPU-bound task goes from nice 0 to
 * nice 1, it will get ~10% less CPU time than another CPU-bound task
 * that remained on nice 0.
 *
 * The "10% effect" is relative and cumulative: from _any_ nice level,
 * if you go up 1 level, it's -10% CPU usage, if you go down 1 level
 * it's +10% CPU usage. (to achieve that we use a multiplier of 1.25.
 * If a task goes up by ~10% and another task goes down by ~10% then
 * the relative distance between them is ~25%.)
 */
static const int prio_to_weight[40] = {
 /* -20 */     88761,     71755,     56483,     46273,     36291,
 /* -15 */     29154,     23254,     18705,     14949,     11916,
 /* -10 */      9548,      7620,      6100,      4904,      3906,
 /*  -5 */      3121,      2501,      1991,      1586,      1277,
 /*   0 */      1024,       820,       655,       526,       423,
 /*   5 */       335,       272,       215,       172,       137,
 /*  10 */       110,        87,        70,        56,        45,
 /*  15 */        36,        29,        23,        18,        15,
};
```

CFS为完美多任务中的无限小调度周期的近似值设定了一个目标，称为“目标延迟”，可以认为就是一个调度周期，代表着同一个进程两次被调度的间隔时间。

现在，假设有两个进程，nice值分别为0和5，那么根据上面的映射数组可知，nice值为0的权重为 1024, nice 值为5的权重为335，差不多3倍关系，那么如果调度周期为20ms，则nice为0的进程将获得

$20*(3/(3+1))=20*(3/4)=15ms$

的处理时间，nice为5的则是5ms. 同理，如果是nice值为10和15的两个进程，权重比也约为3倍，同样分别获得15ms和5ms的处理时间。可见绝对的nice值不再影响调度决策，只有相对值才会影响处理器时间的分配比例。

总结下，任何进程的处理器时间都是有其和其它所有可运行进程的nice值的相对差值决定，nice值对时间片不再是算数加权，而是几何加权。nice值对应的不是绝对时间，而是处理器的使用比。CFS的公平调度是因为它确保每个进程公平的处理器使用比。CFS不是完美的公平，只是近乎完美。但在绝大多数多进程环境下，降低了调度延迟带来的不公平性。

## Linux 调度的实现

CFS的调度算法相关代码位于 `kernel/sched_fair.c` 文件，主要关注其中4个部分。

- 时间记账
- 进程选择
- 调度器入口
- 睡眠与唤醒

### 时间记账

所有的调度器都需要对进程的运行时间记账，也就是说，需要记录当前调度周期内，进程还剩下多少时间片可以用。

**调度器实体结构** `sched_entity` 定义于 `<linux/sched.h>`, 被CFS调度器用于追踪进程运行的时间记账。

```c hl_lines="9"
struct sched_entity {
    struct load_weight load; // 权重，与优先级相关
    struct rb_node run_node; // 红黑树的节点
    struct list_head group_node; // 所在进程组
    unsigned int on_rq; // 标记是否处于红黑树运行队列中

    u64 exec_start; // 进程开始执行的时间
    u64 sum_exec_runtime; // 进程总运行时间
    u64 vruntime; // 虚拟运行时间
    u64 prev_sum_exec_runtime; // 进程在切换CPU时的sum_exec_runtime

    u64 last_wakeup;
    u64 avg_overlap;
    u64 nr_migrations;
    u64 start_runtime;
    u64 avg_wakeup;

/* many stat variables elided, enabled only if CONFIG_SCHEDSTATS is set */
};
```

该结构被嵌入在进程描述符`struct task_struct`中，对应名为`se`的成员变量。

关于上面高亮的部分，也就是 **虚拟运行时间** `vruntime`, 不同于进程的实际运行时间，虚拟运行时间的计算是实际运行时间经过了所有可运行进程总数的标准化（或者说是加权）后的值。以ns为单位，与定时器节拍不再相关。

CFS为了实现理想多任务处理器虚拟出了这个时钟，一个进程的`vruntime`随着运行时间增加而增加，但是增加的速度由其所在的权重决定，其权重又与nice值相关。

权重越高，说明优先级越高，那么`vruntime`的增长速率就越小；反之权重越低，优先级越低，那么`vruntime`的增长速率就越大，感觉时间很快就耗尽了。

下面来看下记账时间的更新，是在文件`kernel/sched_fair.c`的函数`update_curr`中完成的。

```c hl_lines="15 19"
static void update_curr(struct cfs_rq *cfs_rq)
{
    struct sched_entity *curr = cfs_rq->curr;
    u64 now = rq_of(cfs_rq)->clock;
    unsigned long delta_exec;

    if (unlikely(!curr))
        return;

    /*
    * Get the amount of time the current task was running
    * since the last time we changed load (this cannot
    * overflow on 32 bits):
    */
    delta_exec = (unsigned long)(now - curr->exec_start);
    if (!delta_exec)
        return;

    __update_curr(cfs_rq, curr, delta_exec);
    curr->exec_start = now;

    if (entity_is_task(curr)) {
        struct task_struct *curtask = task_of(curr);

        trace_sched_stat_runtime(curtask, delta_exec, curr->vruntime);
        cpuacct_charge(curtask, delta_exec);
        account_group_exec_runtime(curtask, delta_exec);
    }
}
```

`delta_exec` 是进程实际的运行时间，由当前时间减去执行的启动时间得到。

`vruntime`是在`__update_curr`函数中更新的，下面来看看。

```c hl_lines="15 17"
/*
* Update the current task’s runtime statistics. Skip current tasks that
* are not in our scheduling class.
*/
static inline void
__update_curr(struct cfs_rq *cfs_rq, struct sched_entity *curr,
              unsigned long delta_exec)
{
    unsigned long delta_exec_weighted;

    schedstat_set(curr->exec_max, max((u64)delta_exec, curr->exec_max));

    curr->sum_exec_runtime += delta_exec;
    schedstat_add(cfs_rq, exec_clock, delta_exec);
    delta_exec_weighted = calc_delta_fair(delta_exec, curr);

    curr->vruntime += delta_exec_weighted;
    update_min_vruntime(cfs_rq);
}
```

`__update_curr`基于所有可运行进程数对实际运行时间`delta_exec`进行加权，最后将当前进程的`vruntime`值自增这个加权值。这个函数是由系统定时器周期性调用的，无论进程是可执行状态还是被堵塞处于不可运行状态。

因此，`vruntime`可以准确测量给定进程的运行时间，并由此知道下一个被执行的进程。

