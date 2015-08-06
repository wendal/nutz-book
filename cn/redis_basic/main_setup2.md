# 再在MainSetup中添加测试代码

## 打开MainSetup继续添加代码

```java
RedisService redis = ioc.get(RedisService.class);
redis.set("hi", "wendal");
log.debug("redis say again : "  + redis.get("hi"));
```

## 启动tomcat即可看到日志

```
2015-08-07 04:58:41,203 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'redisService'<class net.wendal.nutzbook.service.RedisService>
2015-08-07 04:58:41,203 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:163) DEBUG - 	 >> Load definition
2015-08-07 04:58:41,203 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:144) DEBUG - Found IocObject(redisService) in IocLoader(AnnotationIocLoader@2020547678)
2015-08-07 04:58:41,203 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'redisService'<class net.wendal.nutzbook.service.RedisService>
2015-08-07 04:58:41,204 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'redis'<interface org.nutz.aop.MethodInterceptor>
2015-08-07 04:58:41,205 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:163) DEBUG - 	 >> Load definition
2015-08-07 04:58:41,205 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:144) DEBUG - Found IocObject(redis) in IocLoader(AnnotationIocLoader@2020547678)
2015-08-07 04:58:41,205 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'redis'<interface org.nutz.aop.MethodInterceptor>
2015-08-07 04:58:41,205 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'redis' to [app] 
2015-08-07 04:58:41,205 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'jedisPool'<>
2015-08-07 04:58:41,205 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'redis'<interface org.nutz.aop.MethodInterceptor>
2015-08-07 04:58:41,208 org.nutz.aop.asm.AsmClassAgent.<clinit>(AsmClassAgent.java:29) DEBUG - AsmClassAgent will define class in Version 50
2015-08-07 04:58:41,228 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'redisService' to [app] 
2015-08-07 04:58:41,229 net.wendal.nutzbook.MainSetup.init(MainSetup.java:99) DEBUG - redis say again : wendal
```

## 在其他模块/Service使用redis

* 用RedisService中演示的方式, aop拦截+static import
* 通过'''@Inject JedisPool jedisPool''' 然后try-finally的方式操作Jedis实例