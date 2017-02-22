# 添加jedis

## jedis

* 非常好用的redis java客户端
* 官网 https://github.com/xetorthio/jedis
* 下载地址 https://jfrog.nutz.cn/artifactory/jcenter/redis/clients/jedis
* 2.7.+的版本就可以

## Apache Common Pool 2

* jedis依赖
* 下载地址 https://jfrog.nutz.cn/artifactory/jcenter/org/apache/commons/commons-pool2/
* 版本果断选最新的

## Nutz集成Jedis的小插件

* jedis依赖
* 下载地址 https://jfrog.nutz.cn/artifactory/jcenter/org/nutz/nutz-integration-jedis/
* 版本果断选最新的

## 统统放到WebContent/jars下


## maven配置

```xml
		<dependency>
			<groupId>redis.clients</groupId>
			<artifactId>jedis</artifactId>
			<version>2.8.1</version>
		</dependency>
		<dependency>
			<groupId>org.nutz</groupId>
			<artifactId>nutz-integration-jedis</artifactId>
			<version>1.r.60.r2</version>
		</dependency>
```
