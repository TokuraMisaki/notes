# Eureka 注册中心

## **Eureka是Spring Cloud中负责服务注册和发现的组件**

常见的注册中心
  
|特性|Eureka|Nacos|Consul|Zookeeper|
|---|---|---|---|---|
|CAP|AP|CP+AP|CP|CP|
|雪崩保护|有|有|无|无|
|健康检查|ClientBeat|TCP/HTTP/Mysql/ClientBeat|TCP/Http/gRPC/Cmd|Keep Alive|
|自动注销实例|支持|支持|不支持|不支持|
|访问协议|Http|Http/Dns|Http/Dns|TCP|
|多数据中心|支持|支持|支持|不支持|
|跨平台数据中心|不支持|支持|支持|不支持|
|SpringCloud集成|支持|支持|支持|支持|

## **Eureka三种角色**

1. Eureka Server
    通过Register Get Renew 等接口提供的注册和发现
2. Service Provider
    服务提供者 把自身的服务实例注册到Eureka Server中
3. Service Consumer
    服务消费者 从Eureka Server中获取服务列表 消费服务

> 1.实例化服务  
> 2.将服务注册到注册中心  
> 3.注册中心收录服务  
> 4.从注册中心获取服务列表  
> 5.基于负载均衡算法从地址列表选择一个服务地址进行服务调用  
> 6.定期发动心跳  
> 7.检查没有定期送心跳的服务并在一定时间内剔除服务  

## **Eureka 服务消费的实现**

+ DisCoveryClient: 通过元数据获取服务信息
+ LoadBalacerClient: Ribbon的负载均衡器
+ @LoadBalanced: 通过注解开启Ribbon负载均衡器

*CAP*

+ Consistency  一致性
+ Availability 高可用
+ Partition-Tolerance 分区容错

## **Eureka自我保护**

服务在Eureka注册之后 每30s会发动心跳包 超过90秒没有发动心跳的服务会被定期删除

Eureka Server 收不到微服务的心跳原因

+ 微服务自身原因
+ 微服务与Eureka Server之间的网络故障

Eureka Server在运行期间会统计所有的微服务实例心跳失败比例在15分钟内是否低于85% 如果低于 Eureka Server会将这些实例保护起来,不会剔除这些服务 同时提示一个警告 这就是Eureka Server的自我保护
