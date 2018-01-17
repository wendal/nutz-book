# 关于Maven和MyEclipse的说明

## QQ群里反馈有这些问题及解决方法

* Maven下报配置文件未能找到 -- 提前添加log4j的配置文件到resources文件夹
* MyEclipse下修改UTF-8编码无效 -- 在配置里面修改workspace的编码,及tomcat的JVM启动参数(加入-Dfile.encoding=utf-8)

## Maven项目

在nutz-book-project的源码中, 有pom.xml

推荐的maven mirror, 可大大提高jar下载速度. 注意是https协议.

```xml
<mirrors>
  <mirror>
    <id>nutzcn</id>
    <mirrorOf>central</mirrorOf>
    <name>super mavem mirror for nutz users</name>
    <url>http://jfrog.nutz.cn/artifactory/libs-release</url>
  </mirror>
</mirrors>
```

书中的目录结构,并非maven, 对应关系如下:

|书中的目录名称|maven中的目录名称  |
|-------------|------------------|
|src          |src/main/java     |
|conf         |src/main/resources|
|WebContent   |src/main/webapp   |

常用nutz镜像库及快照版地址

```xml
	<repositories>
		<repository>
			<id>nutz</id>
			<url>https://jfrog.nutz.cn/artifactory/jcenter</url>
		</repository>
		<repository>
			<id>nutz-snapshots</id>
			<url>https://jfrog.nutz.cn/artifactory/snapshots</url>
			<snapshots>
				<enabled>true</enabled>
				<updatePolicy>always</updatePolicy>
			</snapshots>
			<releases>
				<enabled>false</enabled>
			</releases>
		</repository>
	</repositories>
```
