---
title: JDK的命令行工具
tags: 
- JDK的命令行工具
categories:
- JVM
---

# jinfo:查看已经运行的java进程信息
* 查看最大堆内存：jinfo -flag MaxHeapSize 12036 
>例：jinfo -flags 12036
* 查看垃圾收集器：
>jinfo -flag UseConcMarkSweepGC 12036
jinfo -flag UseG1GC 12036
jinfo -flag UseParallelGC 12036


# jstat ：查看JVM统计信息
* 类加载
> jstat -class 12036
* 垃圾收集
> jstat -gc 12036
* JIT编译
>

# jstack:打印JVM所有线程
> jstack 12036