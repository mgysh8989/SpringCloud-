## Eureka 自我保护机制

Eureka中分为两种角色
+ EurekaClient（注册客户端）
+ EurekaServer（注册中心服务端）

为了防止EurekaClient正常运行，但是与EurekaServer网络不通的情况下，EurekaServer不会对EurekaClient服务进行剔除，于是Eureka使用了自我保护机制

#### 自我保护机制：

默认情况下，Client定时会向Server端发送心跳包，来告知Server端服务正常运行。
但是Server端在一定时间（90s）内没有收到Client端发来的心跳包，就会直接从服务注册中剔除该服务
但是在短时间内丢失了大量的服务实例心跳，这是Server端会开启自我保护机制，不会去剔除该服务，防止误剔除