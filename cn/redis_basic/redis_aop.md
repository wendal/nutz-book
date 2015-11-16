# 添加redis拦截器

## 因为JedisPool需要try-finally,所以我们做点改造,用aop的方式演示一种使用方式

新建一个类, net.wendal.nutzbook.util.RedisInterceptor

```java
package net.wendal.nutzbook.util;

import org.nutz.aop.InterceptorChain;
import org.nutz.aop.MethodInterceptor;
import org.nutz.ioc.loader.annotation.Inject;
import org.nutz.ioc.loader.annotation.IocBean;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;

@IocBean(name="redis")
public class RedisInterceptor implements MethodInterceptor {

	@Inject JedisPool jedisPool;
	
	static ThreadLocal<Jedis> TL = new ThreadLocal<Jedis>();
	
	public void filter(InterceptorChain chain) throws Throwable {
		if (TL.get() != null) {
			chain.doChain();
			return;
		}
		try (Jedis jedis = jedisPool.getResource()) {
			TL.set(jedis);
			chain.doChain();
		} finally{
			TL.remove();
		}
	}

	public static Jedis jedis() {
		return TL.get();
	}
}

```

### 这个类的工作方式很简单,就是进入方法之前,取jedis放入ThreadLocal,这样在被拦截的方法内就能通过静态方法 jedis()获取实例,且不需要关心Jedis实例的关闭问题(被拦截的方法执行完毕的时候释放)