# AOP调用过程：
* 配置类上加@EnableAspectJAutoProxy注解
* @EnableAspectJAutoProxy注解使用了@Import(AspectJAutoProxyRegistrar.class)
* AspectJAutoProxyRegistrar类调用registerBeanDefinitions方法
* registerBeanDefinitions方法中调用AopConfigUtils.registerAspectJAnnotationAutoProxyCreatorIfNecessary(registry) 
* registerAspectJAnnotationAutoProxyCreatorIfNecessary中向容器注册名为key为**org.springframework.aop.config.internalAutoProxyCreator**，value是**AnnotationAwareAspectJAutoProxyCreator*，这个类是BeanPostProcessor的子类
* AnnotationAwareAspectJAutoProxyCreator：贯穿了AOP,继承关系如下：
* AnnotationAwareAspectJAutoProxyCreator
	* AspectJAwareAdvisorAutoProxyCreator
		* AbstractAdvisorAutoProxyCreator
			* AbstractAutoProxyCreator  extends ProxyProcessorSupport implements SmartInstantiationAwareBeanPostProcessor, BeanFactoryAware
			* 关注后置处理器，自动装配BeanFactory
* SmartInstantiationAwareBeanPostProcessor:bean的后置处理器
* BeanFactoryAware：能把beanFactory传进来

***
# IOC创建internalAutoProxyCreator的bean，调用过程：
* refresh()
	* registerBeanPostProcessors(beanFactory);
		* PostProcessorRegistrationDelegate.registerBeanPostProcessors(beanFactory, this);
			* AnnotationAwareAspectJAutoProxyCreator实现了Ordered接口，执行对应逻辑
				*  进入beanFactory.getBean(ppName, BeanPostProcessor.class);
					*  doGetBean(name, requiredType, null, false);
						* createBean
							* Object bean = resolveBeforeInstantiation(beanName, mbdToUse);  返回代理对象，会有前置通知后置通知
								* bean = applyBeanPostProcessorsBeforeInstantiation(targetType, beanName);
									* 	Object result = ibp.postProcessBeforeInstantiation(beanClass, beanName); 
										* Object proxy = createProxy(beanClass, beanName, specificInterceptors, targetSource); 产生代理对象
											*  proxyFactory.getProxy(getProxyClassLoader()); 
												* return createAopProxy().getProxy(classLoader);   `proxyFactory有cglib和jdk两种实现`
							
								* Object beanInstance = doCreateBean(beanName, mbdToUse, args);
									* 	instanceWrapper = createBeanInstance(beanName, mbd, args);

***
# AnnotationAwareAspectJAutoProxyCreator利用后置处理器的方法拦截代理方法
* refresh()
	* finishBeanFactoryInitialization(beanFactory);
		* beanFactory.preInstantiateSingletons();
			* 	getBean(beanName);
				* doGetBean
					* createBean
						* Object bean = resolveBeforeInstantiation(beanName, mbdToUse); ：返回被代理类

# AOP过程猜想：
* 1.拦截方法
* 2.调用IOC的createBean()方法
* 3.