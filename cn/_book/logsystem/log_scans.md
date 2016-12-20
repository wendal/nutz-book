# 资源扫描系统的Log

## 把这部分的log摘取出来. 以org.nutz.resource下的log为准

```
2015-03-30 10:49:49,383 org.nutz.resource.Scans.<init>(Scans.java:484) DEBUG - Locations for Scans:
[JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\bootstrap.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\tomcat-juli.jar], JarResourceLocation [jarPath=D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/lib/nutz-1.b.52.jar], FileSystemResourceLocation [root=D:\nutzbook\eclipse], FileSystemResourceLocation [root=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\classes]]
2015-03-30 10:49:49,510 org.nutz.resource.Scans.init(Scans.java:75) DEBUG - Locations for Scans:
[JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\nutz-1.b.52.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\bootstrap.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\tomcat-juli.jar], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\log4j-1.2.17.jar], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\mysql-connector-java-5.1.34.jar], JarResourceLocation [jarPath=D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/lib/nutz-1.b.52.jar], FileSystemResourceLocation [root=D:\nutzbook\eclipse], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\druid-1.0.13.jar], FileSystemResourceLocation [root=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\classes]]
2015-03-30 10:49:49,618 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 1 resource by src( ioc/ ) , regex( ^(.+[.])(js|json)$ )
2015-03-30 10:49:49,625 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
10:49:50,070 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
```

## 分析每条的含义

* 第一条是非Mvc环境下的Scans初始化的日志, 因为Scans类在加载时会先进行自我初始化
* 第二条,是设置ServletContext后,Scans类重新初始化,可以看到找到了Web环境下的classes目录和相关的jar包
* 第三条,是Ioc扫描js配置文件时输出的日志
	* ```DEBUG - Found 1 resource by src( ioc/ ) , regex( ^(.+[.])(js|json)$ )``` 代表在ioc目录下找到1个匹配的文件. 注意,这里的"ioc/"是指classpath下的ioc目录,这点非常重要
* 第四条,是@Modules注解所配置的scanPackage=true所触发的入口类扫描. 强调再强调, 注解只是配置信息,自身无代码操作.注解的实际作用,是取决与读取注解的代码如何理解这个注解,而跟这个注解具体的名字,属性是没有相关性的.
* 第五条,是Ioc扫描注解配置的log.

## 需要明白的几个点

* Modules跟Ioc扫描注解,是2个不同的动作, 因为Nutz中的Mvc与Ioc是分离的, 一个Module类并不强制为一个Ioc对象,反之也是.
* 注解只是配置信息. 如果没有代码去读取注解中的配置信息,这个注解是不会有意义的.

## 关联的文章(选修)

答案均在下一期的今晚来一发

* [@IocBy和@Modules是什么关系?](http://my.oschina.net/wendal/blog/359675)
* [dao.js与IocBean的关系是啥?](http://my.oschina.net/wendal/blog/360081)