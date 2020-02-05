# 一、服务拆分的方法论

如何拆功能

1.单一职责，松耦合，高内聚

2.关注点分离

​	

服务和数据的关系

1.先考虑业务功能，再考虑



# 二、zuul

## 1.pre

限流，鉴权

## 2.post

统计，日志

## 3.高可用

# 三、hystrix

断路器开关：


			@HystrixProperty(name = "circuitBreaker.requestVolumeThreshold", value = "10"),

​			
			@HystrixProperty(name = "circuitBreaker.sleepWindowInMilliseconds", value = "10000"),

​			
			@HystrixProperty(name = "circuitBreaker.errorThresholdPercentage", value = "60") 

# 四、分布式追踪系统

## 1.核心步骤

###1）数据采集

###2）数据存储

### 3）查询展示

## 2.OpenTracing



