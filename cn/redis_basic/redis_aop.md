# 如何使用jedis/redis的aop拦截器

## 未封装的jedis操作比较繁琐

如果你用过jedis, 应该见过这样的写法

```java
Jedis jedis = null;
try {
   jedis = jedisPool.getResource();
	 ....
	 ....
} finally {
   if (jedis != null)
	     jedis.close();
}
```

## nutz提供的aop封装

基于@Aop("redis")实现jedis资源的自动开启与关闭

```java
import static org.nutz.integration.jedis.RedisInterceptor.jedis;

@IocBean
public class UserServiceImpl {

  @Aop("redis")
	public User addUser(User user) {
		  dao.insert(user);
      jedis().incr("user:count");
			return user;
	}
}

```

是不是很清爽呢?

## 如果我希望直接操作JedisPool呢?

推荐使用JedisPool的等价类JedisAgent, 两者的区别如下:

* JedisPool通常是单机或主从,若将来需要切换到JedisCluster(redis 3集群模式), 需要修改所有相关代码
* JedisCluster操作的是redis 3.x集群, API与Jedis不完全兼容,而且不共享超类.
* JedisAgent,与JedisPool类似的API, 根据配置信息(通常指redis.properties),可无缝切换到集群模式
* JedisPool与JedisAgent均通过getResource()方法获取Jedis对象.
* JedisAgent已经预先封装了JedisCluster,无论是单机还是集群,均返回统一的Jedis对象
* 考虑到将来集群的情况, 建议避免使用pipeline/事务/lua.

```java
import static org.nutz.integration.jedis.RedisInterceptor.jedis;

@IocBean
public class UserServiceImpl {

	@Inject JedisAgent jedisAgent; // 同理,可以是JedisPool和JedisCluster

	public User addUser(User user) {
		  dao.insert(user);
		  try (Jedis jedis = jedisAgent.getResource()){
          jedis().incr("user:count");
			}
			return user;
	}
}
```
