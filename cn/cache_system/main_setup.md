# MainSetup关联

为了排错的需要,在MainSetup中获取CacheManager
--------

```java
		CacheManager cacheManager = ioc.get(CacheManager.class);
		log.debug("Ehcache CacheManager = " + cacheManager);
```

事实上现在就能启动项目看看日志(如果你比较着急的话), 类似于:

```log
2015-05-22 10:00:56,421 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'cacheManager'<class net.sf.ehcache.CacheManager>
2015-05-22 10:00:56,421 net.wendal.nutzbook.MainSetup.init(MainSetup.java:59) DEBUG - Ehcache CacheManager = nutzbook
```

如果出错,检查ehcache.xml,shiro.ini的配置是否正确, 及ehcache.js中的是否对应了ehcache.xml中的类