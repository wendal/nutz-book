# 添加RedisService

## 新建一个类net.wendal.nutzbook.service.RedisService

```java
package net.wendal.nutzbook.service;

import static net.wendal.nutzbook.util.RedisInterceptor.*; // 静态导入哦

import org.nutz.ioc.aop.Aop;
import org.nutz.ioc.loader.annotation.IocBean;

@IocBean
public class RedisService {
	
	@Aop("redis")
	public void set(String key, String val) {
		jedis().set(key, val);
	}

	@Aop("redis") // 加上这个拦截器后jedis()才能返回Jedis实例哦
	public String get(String key) {
		return jedis().get(key);
	}
}

```