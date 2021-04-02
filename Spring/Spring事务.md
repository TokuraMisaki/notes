[[事务]]
+	编程式事务(通过代码实现事务)
+	声明式事务(通过配置实现事务)

[[事务隔离级别]]


**事务传播行为**
+ propagation_required
	如果存在事务则加入,不存在则新建
+ propagation_required_new
	新建事务,如果当前存在事务则挂起
+ propagation_suports
	支持事务 如果存在则加入 不存在则以非事务方式运行 
+ propagation_not_supports
	不支持事务,如果存在事务则挂起
+ propagation_mandatory
	使用当前事务,如果没有事务则抛出异常
+ propagation_never
	以非事务方式运行,如果存在事务抛出异常
+ propagation_nester
	如果存在事务则嵌套,不存在则和propagation_required一样
	