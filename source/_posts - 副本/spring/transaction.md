---
title: spring事务
tags: 
- spring
categories:
- spring
---

# 接口
	* PlatformTransactionManager
	* TransactionDefinition
	* TransactionStatus
# ACID:
	* 原子性
	* 一致性
	* 隔离性
	* 持久行
# 传播行为
	* Progation_Required
	* Progation_Suppport
	* Progation_manatory
	* Progation_Required_new
	* Progation_not_support
	* Progation_never
	* Progation_nested :spring特有的
		* 连接点
# 隔离级别
	* Isolation_NOT_COMMITED
	* ISolation_COMMITED
	* Isolation_Repeatable_read
	* Isolation_Serilizable
# 并发访问问题：
	* 脏读：读到其他事务还没提交的数据，数据被回滚后，引起的问题
	* 不可重复读：两次都读取结果不一致，读到的数据被其他事务修改后，再去读取，会不一样
	* 幻读：也是两次读取结果不一致，读取到的数据后，其他数据有插入或者删除，再去读取，会不一样
# 原理：Spring AOP