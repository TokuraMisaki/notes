# Spring源码解析

在refresh方法的AbstractApplicationContext#finishBeanFactoryInitialization
里面的DefaultListableBeanFactory#preInstantiateSingletons方法里面实现bean的创建
在preInstantiateSingletons方法里面会将beanDefinitionNames复制一个副本 然后遍历这个副本 现在只对其中非工厂bean的创建进行介绍 getBean --> doGetBean
doGetBean里面首先对beanName进行一次转化 这里先不整理以普通bean为例.
然后getSingleton检查单例池里面是否已经存在bean 下面解析getSingleton源码

## getSingleton()

```
protected Object getSingleton(String beanName, boolean allowEarlyReference) {
        //第一步先去单例池看bean存不存在
		Object singletonObject = this.singletonObjects.get(beanName);
  //如果单例池里面不存在bean 并且当前bean正在创建
		//再去earlySingletonObjects里面拿 如果没有
		//去singletonFactory拿 如果有将对象放到earlySingletonObjects里面 从singletonFactory里面移除
        //为什么这么做?
		if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
			synchronized (this.singletonObjects) {
				singletonObject = this.earlySingletonObjects.get(beanName);
				if (singletonObject == null && allowEarlyReference) {
					ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
					if (singletonFactory != null) {
						singletonObject = singletonFactory.getObject();
						this.earlySingletonObjects.put(beanName, singletonObject);
						this.singletonFactories.remove(beanName);
					}
				}
			}
		}
		return singletonObject;
	}
```
