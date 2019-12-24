#高级特性

##死信队列

DLX,Dead-Letter-Exchange

```
利用DLX，当消息在一个队列中变成死信（dead message）之后，它能被重新publish到另一个Exchange，这个Exchange就是DLX
```

消息变成死信有以下几种情况：

1）消息被拒绝（basic.reject/basic.nack）并且requeue=false

2）消息TTL过期

3）队列达到最大长度

# 集群

## 主备模式

实现RabbitMQ的高可用集群，一般在并发和数据量不高的情况下，这种模型非常的好用且简单。主备模式也称为Warren模式。

主备和主从的区别：

主备的备节点只提供备份，不提供读功能；主从的从节点对外可读。

## 远程模式

远距离通信和复制，所谓Shovel就是我们可以把消息进行不同数据中心的复制工作，我们可以跨地域的让两个mq集群互联。

## 镜像模式

## 多活模式



