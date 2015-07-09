# 配置shiro.ini

打开conf目录下的shiro.ini,在[main]节点的末尾,加入
------------------------------------------------

```ini
cacheManager = org.apache.shiro.cache.ehcache.EhCacheManager
cacheManager.cacheManagerConfigFile=classpath:ehcache.xml
nutzdao_realm.cacheManager = $cacheManager
```

留意一下配置文件的路径,指向的就是上一小节定义的ehcache,并且让nutzdao_realm引用这个缓存管理器.

如果需要缓存shiro的Session,可以加入这些配置(不推荐)
------------------------------------------------

```xml
sessionDAO = org.apache.shiro.session.mgt.eis.EnterpriseCacheSessionDAO
sessionManager.sessionDAO = $sessionDAO
securityManager.sessionManager = $sessionManager

securityManager.cacheManager = $cacheManager
```