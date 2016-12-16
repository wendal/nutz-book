# 下载jar包

nutz本身并不强制依赖第三方的jar,但项目需要还是会加入下列的jar

### Nutz本身

* 不需要废话了
* [下载地址](http://maven.nutz.cn/nexus/content/repositories/central/org/nutz/nutz/1.r.59/nutz-1.r.59.jar)

### Mysql数据库驱动

* Mysql作为本书选用的数据库,那它的驱动当然是必不可少的
* 若使用6.x版本的驱动的话,务必使用最新版的druid
* [下载地址](http://maven.nutz.cn/nexus/content/repositories/central/mysql/mysql-connector-java/5.1.40/mysql-connector-java-5.1.40.jar)

### 数据库连接池Druid

* 我个人一直推荐与Nutz一起使用的数据库连接池,带强大的监控功能
* [下载地址](http://maven.nutz.cn/nexus/content/repositories/central/com/alibaba/druid/1.0.26/druid-1.0.26.jar)

### 关于Log4j

* 如果你执意要加入log4j.jar,那么务必要将其配置log4j.properties配置好, 而且均为debug级别,以免遗漏本书提及的内容.
* 但maven用户,就必须先加入log4j.jar了, 而且把log4j.properties配置好. 下面是推荐配置

```
log4j.rootLogger=debug,Console

log4j.appender.Console=org.apache.log4j.ConsoleAppender
log4j.appender.Console.layout=org.apache.log4j.PatternLayout
log4j.appender.Console.layout.ConversionPattern=[%-5p] %d{HH:mm:ss.SSS} %l - %m%n
```