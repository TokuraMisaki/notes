#  Feign声明式服务调用

Feign是Spring Cloud Netflix 组件中一个轻量级RESTful的HTTP服务客户端 实现了负载均衡和Rest调用的开源框架 封装了Ribbon和RestTemplate 实现了WebService的面向接口编程 进一步降低了项目的耦合度

+ Feign 内置了Ribbon 用来做客户端的负载均衡和调用服务注册中心的服务
+ Feign本身不支持Spring MVC的注解 Spring cloud开发了OpenFeign
+ Feign是一种声明式 模板化的Http客户端 (仅在Consumer中使用)
+ Feign的使用: 使用Feign的注解定义接口,调用这个接口,就可以调用服务注册中心的服务

> + 启动时 程序会扫描包下所有**@FeignClient**注解的类,并将这些类注入到Spring的IOC容器中,当定义的Feign接口被调用时,通过JDK的动态代理生成RequestTemplate
> + RequestTemplate中包含请求的所有信息 
> + RequestTemplate 生成Request 将Request交给client处理 这个client默认是JDK的HTTPUrlTemplate 也可以是OKHTTP或Apache的HTTPClient
> + 最后client封装成LoadBalanceClient 结合Ribbon负载均衡发起调用

##  Feign远程调用基本流程

 Feign远程调用核心就是通过一系列封装和处理,将以Java注解的方式定义的远程调用API接口,最终转换成HTTP的请求形式,将HTTP请求的相应结果,解码成Java Bean,返回给调用者



