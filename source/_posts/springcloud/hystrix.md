#资源隔离

hystrix进行资源隔离，其实是提供了一个抽象，叫做command，就是说，你如果要把对某一个依赖服务的所有调用请求，全部隔离在同一份资源池内。对这个依赖服务的所有调用请求，全部走这个资源池内的资源，不会去用其他的资源了，这个就叫做资源隔离。

hystrix最基本的资源隔离技术，线程池隔离技术。

另外一种隔离方式是信号量隔离。

区别：

## 1. 线程池隔离

舱壁隔离



# 批量接口

HystrixObservableCommand

# command的四种方式

execute

queue



# 几个概念

command key：代表了一类command，一般来说，代表了底层的依赖服务的一个接口

command group：代表了某一个底层的依赖服务，

一般来说，推荐是根据一个服务去划分出一个线程池，command key默认属于同一个线程池。

#降级的分类

## 1.自动降级

超时，失败次数，故障，限流

## 2.人工降级

秒杀，双11大促等

# 短路器

##1.工作原理

1. 如果经过短路器的流量超过一定的阈值，HystrixCommandProperties.circuitBreakerRequestVolumeThreshold，默认20

   比如，要求10s内，经过短路器的流量必须到达20个；在10s内，经过短路器的流量才10个，那么根本不会去判断要不要短路。

2. 如果短路器统计到的异常调用的占比超过了一定的阈值，HystrixCommandProperties.circuitBreakerErrorThresholdPercentage，默认50

3. 然后短路器从close状态转换到open状态

4. 短路器打开时，所有经过该短路器的请求全部被短路，不调用后端服务，直接走fallback降级

5. 经过一段时间之后，HystrixCommandProperties.circuitBreakerSleepWindowInMilliseconds，会half-open，让一条请求经过短路器，看能不能正常调用，如果调用成功了，那么久自动恢复，转到close状态

##2.配置

(1) circuitBreaker.enabled

​	是否开启短路器,默认为true

(2) circuitBreaker.requestVolumeThreshold

​	滑动窗口内，请求最少达到以后才能开启短路器，默认20

(3) circuitBreaker.sleepWindowInMilliseconds

​	设置在短路之后，需要在多长时间内直接reject请求，然后在这段请求之后，再重新到half-open状态，尝试允许请求通过一级自动恢复；默认50ms

(4) circuitBreaker.errorThresholdPercentage

设置异常请求量的百分比，当异常请求达到这个百分比时，就触发打开短路器，默认是50，也就是50%

 (5) circuitBreaker.forceOpen



