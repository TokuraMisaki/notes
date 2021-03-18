# Ribbon负载均衡

**Ribbon 是基于Http和TCP的客户端负载均衡工具**

负载均衡方案

+ 集中式负载均衡(服务器负载均衡) 在Consumer和Provider 中使用独立的负载均衡措施 改设施负载把访问请求通过某种策略发送到Provider
+ 进程内负载均衡(客户端负载均衡) 将负载均衡集成到Consumer Consumer从服务注册中心获知有哪些地址可用 然后自己再从中找出合适的Provider
  
  *Ribbon属于进程内负载均衡*

Ribbon 负载均衡策略

+ **轮询 RoundRobinRule**   
  依次获取下一个Provider
+ **权重轮询 WeightResponseRule**  
  根据Provider响应时间分配权重 时间越长 权重越小 被选中的概率越小
+ **随机  RandomRule**  
  随机
+ **最少并发 BestAvailableRule**  
  选择正在请求中的并发数最小的Provider
+ **重试 RetryRule**  000
  轮询的加强版 如果服务不可用回去尝试其他节点
+ **可用性敏感 AvailablityFilterRule**  
  过滤掉性能差的Provider
  + 过滤掉Eureka 中0一直连接失败的Provider
  + 过滤掉一直处于高并发的Provider
+ **区域敏感 ZoneAvoidanceRule**
  以一个区域为单位考察可用性 对于不可用的区域整个丢弃 如果这个ip区域中一个或多个实例不可达或变慢 都会降低这个ip区域中其他ip选用概率
