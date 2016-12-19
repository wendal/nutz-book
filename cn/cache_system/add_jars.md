# 添加相关的Jar


下载daocache
----------------------------

* DaoCache并不在Nutz核心包内,而是作为一个插件提供
* 地址 http://repo1.maven.org/maven2/org/nutz/nutz-plugins-daocache/
* 项目地址 https://github.com/nutzam/nutzmore/tree/master/nutz-plugins-daocache
* 该插件还在不停完善中,请下载最新版本

Ehcache 2.x
----------------------------

* 官网 http://ehcache.org/
* 下载地址 http://ehcache.org/downloads/catalog
* 当前最新版本是2.10.0,下载完整版就好了

maven配置
----------------------------

```xml
		<dependency>
			<groupId>org.nutz</groupId>
			<artifactId>nutz-plugins-daocache</artifactId>
			<version>1.r.59</version>
		</dependency>
		<dependency>
			<groupId>net.sf.ehcache</groupId>
			<artifactId>ehcache</artifactId>
			<version>2.10.1</version>
		</dependency>
```
