# 在MainSetup中添加测试代码

下面的代码算是测试redis-jedis-nutz组合的最小测试代码,请不要忽略它们.

## 打开MainSetup类,添加如下代码

```java
		JedisAgent jedisAgent = ioc.get(JedisAgent.class);
		try (Jedis jedis = jedisAgent.getResource()) { // Java7的语法
			String re = jedis.set("_nutzbook_test_key", "http://nutzbook.wendal.net");
			log.debug("redis say : " + re);
			re = jedis.get("_nutzbook_test_key");
			log.debug("redis say : " + re);
		} finally {}
```

## 启动tomcat, 观察日志,正常输出应该是

```
2015-08-07 04:23:51,325 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'jedisPool'<class redis.clients.jedis.JedisPool>
2015-08-07 04:23:51,325 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:163) DEBUG - 	 >> Load definition
2015-08-07 04:23:51,325 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=jedisPool
2015-08-07 04:23:51,325 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:144) DEBUG - Found IocObject(jedisPool) in IocLoader(JsonLoader@1709213544)
2015-08-07 04:23:51,325 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'jedisPool'<class redis.clients.jedis.JedisPool>
2015-08-07 04:23:51,333 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:83) DEBUG - class redis.clients.jedis.JedisPool , no config to enable AOP for this type.
2015-08-07 04:23:51,333 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'jedisPool' to [app]
2015-08-07 04:23:51,333 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'jedisPoolConfig'<>
2015-08-07 04:23:51,334 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:163) DEBUG - 	 >> Load definition
2015-08-07 04:23:51,334 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=jedisPoolConfig
2015-08-07 04:23:51,334 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:144) DEBUG - Found IocObject(jedisPoolConfig) in IocLoader(JsonLoader@1709213544)
2015-08-07 04:23:51,334 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'jedisPoolConfig'<>
2015-08-07 04:23:51,335 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:83) DEBUG - class redis.clients.jedis.JedisPoolConfig , no config to enable AOP for this type.
2015-08-07 04:23:51,335 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'jedisPoolConfig' to [app]
2015-08-07 04:23:51,335 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,335 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,335 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,335 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,336 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'jedisPoolConfig'<>
2015-08-07 04:23:51,336 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,336 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,336 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,336 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:143) DEBUG - Get 'conf'<>
2015-08-07 04:23:51,371 net.wendal.nutzbook.MainSetup.init(MainSetup.java:90) DEBUG - redis say : OK
2015-08-07 04:23:51,372 net.wendal.nutzbook.MainSetup.init(MainSetup.java:92) DEBUG - redis say : http://nutzbook.wendal.net
```

### 最后2行就是读写redis的结果,前面的都是ioc的日志

## 可能遇到的问题

* redis没启动导致读写失败
