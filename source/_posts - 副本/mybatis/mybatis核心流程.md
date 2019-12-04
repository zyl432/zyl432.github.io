---
title: mybatis核心流程
tags: 
- mybatis
categories:
- mybatis
---

# mybatis核心流程三大阶段
* 初始化阶段
> 读取XML配置文件和注解中的配置信息，创建配置对象，并完成各个模块的初始化工作

* 代理阶段
> 封装iBatis的编程模型，使用mapper接口开发的初始化工作

* 数据读写阶段
> 通过SqlSession完成SQL解析，参数的映射，SQL的执行，结果的解析过程