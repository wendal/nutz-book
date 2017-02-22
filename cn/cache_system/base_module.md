# 修改BaseModule

修改一下BaseModule,让它也能访问CacheManager
----

```java
	@Inject
	protected CacheManager cacheManager;
```

一如既往地走默认注入规则: 与属性同名的bean
