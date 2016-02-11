# 下载jar包

nutz本身并不强制依赖第三方的jar,但项目需要还是会加入下列的jar

### Nutz本身

* 不需要废话了
* [下载地址](http://repo1.maven.org/maven2/org/nutz/nutz/1.b.53/nutz-1.b.53.jar)

### Mysql数据库驱动

* Mysql作为本书选用的数据库,那它的驱动当然是必不可少的
* [下载地址](http://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.37/mysql-connector-java-5.1.37.jar)

### 数据库连接池Druid

* 我个人一直推荐与Nutz一起使用的数据库连接池,带强大的监控功能
* [下载地址](http://repo1.maven.org/maven2/com/alibaba/druid/1.0.16/druid-1.0.16.jar)

### 关于Log4j

* 如果你执意要加入log4j.jar,那么务必要将其配置log4j.prop或log4j.xml配置好, 而且均为debug级别,以免遗漏本书提及的内容.