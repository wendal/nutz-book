# 添加ehcache.js

在conf/ioc目录下添加ehcache.js, 作用是将Ehcache声明为一个bean,这样其他模块/Service就能使用它了
--------------

```json
var ioc = {
		cacheManager : {
			type : "net.sf.ehcache.CacheManager",
			factory : "net.sf.ehcache.CacheManager#getCacheManager",
			args : ["nutzbook"] // 对应shiro.ini中指定的ehcache.xml中定义的name
		}
		/*      
		// 如果不需要shiro初始化的Ehcache, 使用下面的方式配置
		cacheManager : {
			type : "net.sf.ehcache.CacheManager",
			factory : "net.sf.ehcache.CacheManager#create"
		}
		 */
};
```

留意一下注释里面的内容哦