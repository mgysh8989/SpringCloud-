## Feign客户端调用

Springcloud支持两种客户端调用工具
1. Rest：RestTemplate 很少使用
2. Feign客户端工具，使用较多

Feign是一个声明式的Http客户端调用工具，采用接口+注解方式实现，易读性较强

Feign客户端调用重点,重构接口信息
示例：
>com.demo.parent 			(存放共同依赖信息)
---
>>com.demo.api 				(只存放接口，没有实现)
---
>>>com.demo.api.service1 	(服务1的接口声明)<br>
>>>com.demo.api.service2 	(服务2的接口声明)<br>
---
>>com.demo.api.service1-impl (服务1API接口的实现)<br>
>>com.demo.api.service2-impl (服务2API接口的实现)


### 服务雪崩效应

默认情况下，Tomcat只有一个线程池处理客户端所有服务请求，在高并发情况下，如果客户端所有请求堆积到统一服务接口上，就会产生Tomcat的所有线程去处理该服务接口，可能会导致其他服务接口无法访问。

如果在Feign客户端的情况下，相应时间过长的时间会引发超时异常，
可以设置延长超时时间

注意，Feign的超时时间是Ribbon和Hystrix的时间和

