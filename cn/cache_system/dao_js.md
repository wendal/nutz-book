# 改造dao.js

重头戏来了,打开conf/ioc/dao.js, 修改dao的定义
---

```json
		dao : {
			type : "org.nutz.dao.impl.NutDao", 
			args : [{refer:"dataSource"}],
			fields : {
				interceptors : [{refer:"cacheExecutor"}, "log"]
			}
		},
		cacheExecutor : {
			type : "org.nutz.plugins.cache.dao.DaoCacheInterceptor",
			fields : {
				cacheProvider : {refer:"cacheProvider"},
                // 需要缓存的表名
				cachedTableNames : ["t_user_profile",
				                    //"t_user", "t_role", "t_permission", "t_role_permission"
				                    ]
			}
		},
		// 基于Ehcache的DaoCacheProvider
		cacheProvider : {
			type : "org.nutz.plugins.cache.dao.impl.provider.EhcacheDaoCacheProvider",
			fields : {
				cacheManager : {refer:"cacheManager"} // 引用ehcache.js中定义的CacheManager
			},
			events : {
				create : "init"
			}
		}
```

关注点
------------------

* 当前的daocache支持单表缓存,注意是表,不是Pojo哦
* NutDaoExt属于原NutDao的补丁版本哦,1.b.53之后直接引用NutDao就行,不需要NutDaoExt
* 当前配置仅缓存t_user_profile
* 请充分了解缓存导致的问题: 缓存数据不同步,缓存竞争存取等等