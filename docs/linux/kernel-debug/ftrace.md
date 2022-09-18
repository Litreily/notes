# Ftrace

## Description

> Ftrace is an internal tracer designed to help out developers and
> designers of systems to find what is going on inside the kernel.
> It can be used for debugging or analyzing latencies and
> performance issues that take place outside of user-space.

## enable related config

1. From "make menuconfig", go to --> "Global Build Settings" then go to --> "Compile kernel with tracing support"
2. In the "Compile kernel with tracing support", enable the below options :-
    - Enable/disable function tracing dynamically
    - Trace process context switches and events
    - Function tracer
3. Once above changes are done, then from the "make kernel_menuconfig", go to --> "Kernel hacking" --> then enable the below options in "Tracers":-
    - Kernel Function Tracer
    - enable/disable function tracing dynamically

## check enable status

``` sh
ls /sys/kernel/debug/tracing/
```

## enable ftrace on runtime

``` sh
#********************************************#
# enable ftrace
#********************************************#
# To enable function tracing during run time
echo 0 > /sys/kernel/debug/tracing/tracing_on
echo function > /sys/kernel/debug/tracing/current_tracer
echo 1 > /sys/kernel/debug/tracing/tracing_on

# To enable specific events to be traced
echo tlet_entry >> /sys/kernel/debug/tracing/set_event
echo tlet_exit >> /sys/kernel/debug/tracing/set_event
echo irq_handler_entry >> /sys/kernel/debug/tracing/set_event
echo irq_handler_exit >> /sys/kernel/debug/tracing/set_event
echo softirq_entry >> /sys/kernel/debug/tracing/set_event
echo softirq_exit >> /sys/kernel/debug/tracing/set_event
echo timer_expire_entry >> /sys/kernel/debug/tracing/set_event
echo timer_expire_exit >> /sys/kernel/debug/tracing/set_event
echo sched_switch >> /sys/kernel/debug/tracing/set_event

# To Dump the FTrace to the console in case of oops
echo 1 > /proc/sys/kernel/ftrace_dump_on_oops

# To increase the size of Ftrace buffer per CPU
echo 2048 > /sys/kernel/debug/tracing/buffer_size_kb

# To enable tracing of signals
echo SyS_reboot:dump > /sys/kernel/debug/tracing/set_ftrace_filter
echo 1 > /sys/kernel/debug/tracing/events/signal/enable
echo 1 > /sys/kernel/debug/tracing/tracing_on
sysctl -w kernel.ftrace_dump_on_oops=1
```
