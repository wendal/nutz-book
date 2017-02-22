# 在IocBy中启用jedis插件

## 只需要简单添加一下即可

```java
@IocBy(args={
  "*js", "ioc/",
  "*anno", "net.wendal.nutzbook",
  "*quartz",
  "*jedis", // 添加这一行
  ""})
```

`*jedis` 代表 org.nutz.integration.jedis.JedisIocLoader

它会负责加载jedis相关的所有配置,不再需要自行添加js和aop 拦截器
