+ ThreadLocal的Key为什么是弱引用

> ThreadLocalMap存储格式是Entry<ThreadLocal,T>
> java中引用传递是对象的副本 如果使用强引用，当原来key对象失效的时候，jvm不会回收map里面的ThreadLocal