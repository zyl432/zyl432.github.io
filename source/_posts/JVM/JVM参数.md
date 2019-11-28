---
title: JVM参数
tags: 
- JVM参数
categories:
- JVM
---

# X参数：非标准化参数
* -Xint：解释执行
* -Xcomp:第一次使用就编译成本地代码
* -Xmixed：混合模式，JVM自己来决定是否编译成本地代码

# 查看JVM运行时的参数
* -XX:+PrintFlagsInitial
> 例如：java -XX:+PrintFlagsFinal -version
* -XX:+PrintFlagsFinal
* -XX:+UnlockExperimentalVMOptions  ----解锁实验参数
* -XX:+UnlockDiagnosticVMOptions  ----解锁诊断参数
* -XX:+PrintCommandLineFlags  ----打印命令行参数