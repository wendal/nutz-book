# 日志总览

下面是当前项目的完整Nutz日志(不包含容器自身的日志),洋洋洒洒81行,各种丰富的信息

```
ALL Nutz Log via Log4jLogAdapter
2015-03-30 10:49:49,321 org.nutz.log.Logs.<clinit>(Logs.java:20) INFO  - Nutz is licensed under the Apache License, Version 2.0 .
Report bugs : https://github.com/nutzam/nutz/issues
2015-03-30 10:49:49,327 org.nutz.mvc.NutFilter.init(NutFilter.java:71) INFO  - NutFilter[nutz] starting ...
2015-03-30 10:49:49,383 org.nutz.resource.Scans.<init>(Scans.java:484) DEBUG - Locations for Scans:
[JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\bootstrap.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\tomcat-juli.jar], JarResourceLocation [jarPath=D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/lib/nutz-1.b.52.jar], FileSystemResourceLocation [root=D:\nutzbook\eclipse], FileSystemResourceLocation [root=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\classes]]
2015-03-30 10:49:49,510 org.nutz.resource.Scans.init(Scans.java:75) DEBUG - Locations for Scans:
[JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\nutz-1.b.52.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\bootstrap.jar], JarResourceLocation [jarPath=D:\nutzbook\apache-tomcat-8.0.20\bin\tomcat-juli.jar], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\log4j-1.2.17.jar], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\mysql-connector-java-5.1.34.jar], JarResourceLocation [jarPath=D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/lib/nutz-1.b.52.jar], FileSystemResourceLocation [root=D:\nutzbook\eclipse], JarResourceLocation [jarPath=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\lib\druid-1.0.13.jar], FileSystemResourceLocation [root=D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\classes]]
2015-03-30 10:49:49,514 org.nutz.mvc.config.AbstractNutConfig.getMainModule(AbstractNutConfig.java:119) DEBUG - MainModule: <net.wendal.nutzbook.MainModule>
2015-03-30 10:49:49,523 org.nutz.mvc.config.AbstractNutConfig.createLoading(AbstractNutConfig.java:50) DEBUG - Loading by class org.nutz.mvc.impl.NutLoading
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:55) INFO  - Nutz Version : 1.b.52 
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:56) INFO  - Nutz.Mvc[nutz] is initializing ...
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:60) DEBUG - Web Container Information:
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:61) DEBUG -  - Default Charset : UTF-8
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:62) DEBUG -  - Current . path  : D:\nutzbook\eclipse\.
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:63) DEBUG -  - Java Version    : 1.8.0_31
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:64) DEBUG -  - File separator  : \
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:65) DEBUG -  - Timezone        : Asia/Shanghai
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:66) DEBUG -  - OS              : Windows 7 amd64
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:67) DEBUG -  - ServerInfo      : Apache Tomcat/8.0.20
2015-03-30 10:49:49,528 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:68) DEBUG -  - Servlet API     : 3.1
2015-03-30 10:49:49,528 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:70) DEBUG -  - ContextPath     : /nutzbook
2015-03-30 10:49:49,529 org.nutz.mvc.config.AbstractNutConfig.getMainModule(AbstractNutConfig.java:119) DEBUG - MainModule: <net.wendal.nutzbook.MainModule>
2015-03-30 10:49:49,529 org.nutz.mvc.impl.NutLoading.createContext(NutLoading.java:217) DEBUG - >> app.root = D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook
2015-03-30 10:49:49,599 org.nutz.castor.Castors.reload(Castors.java:116) DEBUG - Using 91 castor for Castors
2015-03-30 10:49:49,603 org.nutz.mvc.impl.NutLoading.createIoc(NutLoading.java:354) DEBUG - @IocBy(type=org.nutz.mvc.ioc.provider.ComboIocProvider, args=["*js", "ioc/", "*anno", "net.wendal.nutzbook", "*tx"])
2015-03-30 10:49:49,618 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 1 resource by src( ioc/ ) , regex( ^(.+[.])(js|json)$ )
2015-03-30 10:49:49,618 org.nutz.ioc.loader.json.JsonLoader.<init>(JsonLoader.java:44) DEBUG - loading ioc js config from [dao.js]
2015-03-30 10:49:49,622 org.nutz.ioc.loader.json.JsonLoader.<init>(JsonLoader.java:52) DEBUG - Loaded 2 bean define from path=[ioc/] --> [dataSource, dao]
2015-03-30 10:49:49,625 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-03-30 10:49:49,638 org.nutz.ioc.loader.annotation.AnnotationIocLoader.addClass(AnnotationIocLoader.java:83) DEBUG - Found a Class with Ioc-Annotation : class net.wendal.nutzbook.module.UserModule
2015-03-30 10:49:49,652 org.nutz.ioc.loader.annotation.AnnotationIocLoader.<init>(AnnotationIocLoader.java:60) INFO  - Scan complete ! Found 1 classes in 1 base-packages!
beans = ["userModule"]
2015-03-30 10:49:49,652 org.nutz.ioc.loader.json.JsonLoader.<init>(JsonLoader.java:36) DEBUG - Loaded 5 bean define from reader --
[txREPEATABLE_READ, txSERIALIZABLE, txNONE, txREAD_UNCOMMITTED, txREAD_COMMITTED]
2015-03-30 10:49:49,661 org.nutz.mvc.config.AbstractNutConfig.getMainModule(AbstractNutConfig.java:119) DEBUG - MainModule: <net.wendal.nutzbook.MainModule>
2015-03-30 10:49:49,665 org.nutz.mvc.impl.NutLoading.evalUrlMapping(NutLoading.java:143) INFO  - Build URL mapping by org.nutz.mvc.impl.UrlMappingImpl ...
2015-03-30 10:49:49,667 org.nutz.mvc.impl.NutLoading.createViewMakers(NutLoading.java:344) DEBUG - @Views(DefaultViewMaker)
2015-03-30 10:49:49,675 org.nutz.mvc.impl.NutLoading.createChainMaker(NutLoading.java:245) DEBUG - @ChainBy(org.nutz.mvc.impl.NutActionChainMaker)
2015-03-30 10:49:49,679 org.nutz.mvc.impl.Loadings.scanModules(Loadings.java:98) DEBUG - module class location 'file:/D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/classes/net/wendal/nutzbook/MainModule.class'
2015-03-30 10:49:49,679 org.nutz.mvc.impl.Loadings.scanModuleInPackage(Loadings.java:126) DEBUG -  > scan 'net.wendal.nutzbook'
2015-03-30 10:49:49,681 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-03-30 10:49:49,682 org.nutz.mvc.impl.Loadings.checkModule(Loadings.java:140) DEBUG -    >> add 'net.wendal.nutzbook.module.UserModule'
2015-03-30 10:49:49,698 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/'                    >> UserModule.index(...)          : void       | @Ok(jsp:jsp.user.list) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,714 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/add'                 >> UserModule.add(...)            : Object     | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,715 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/count'               >> UserModule.count(...)          : int        | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,716 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/update'              >> UserModule.update(...)         : Object     | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,720 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/delete'              >> UserModule.delete(...)         : Object     | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,724 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/query'               >> UserModule.query(...)          : Object     | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,726 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/login'               >> UserModule.login(...)          : Object     | @Ok(json:{locked:'password|salt',ignoreNull:true}) @Fail(http:500) | by 0 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,727 org.nutz.mvc.impl.UrlMappingImpl.printActionMapping(UrlMappingImpl.java:130) DEBUG -    '/user/logout'              >> UserModule.logout(...)         : void       | @Ok(>>:/ ) @Fail(http:500) | by 1 Filters | (I:UTF-8/O:UTF-8)
2015-03-30 10:49:49,728 org.nutz.mvc.impl.NutLoading.evalUrlMapping(NutLoading.java:203) INFO  - Found 8 module methods
2015-03-30 10:49:49,728 org.nutz.mvc.impl.NutLoading.evalLocalization(NutLoading.java:309) DEBUG - @Localization not define
2015-03-30 10:49:49,729 org.nutz.mvc.impl.NutLoading.evalSetup(NutLoading.java:253) INFO  - Setup application...
2015-03-30 10:49:49,729 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'dao'<interface org.nutz.dao.Dao>
2015-03-30 10:49:49,730 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:166) DEBUG - 	 >> Load definition
2015-03-30 10:49:49,732 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=dao
2015-03-30 10:49:49,736 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:137) DEBUG - Found IocObject(dao) in IocLoader(JsonLoader@1168025266)
2015-03-30 10:49:49,737 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'dao'<interface org.nutz.dao.Dao>
2015-03-30 10:49:49,750 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:82) DEBUG - class org.nutz.dao.impl.NutDao , no config to enable AOP for this type.
2015-03-30 10:49:49,750 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'dao' to [app] 
2015-03-30 10:49:49,753 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'dataSource'<>
2015-03-30 10:49:49,753 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:166) DEBUG - 	 >> Load definition
2015-03-30 10:49:49,753 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=dataSource
2015-03-30 10:49:49,758 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:137) DEBUG - Found IocObject(dataSource) in IocLoader(JsonLoader@1168025266)
2015-03-30 10:49:49,758 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'dataSource'<>
2015-03-30 10:49:49,777 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:82) DEBUG - class com.alibaba.druid.pool.DruidDataSource , no config to enable AOP for this type.
2015-03-30 10:49:49,777 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'dataSource' to [app] 
2015-03-30 10:49:49,811 com.alibaba.druid.pool.DruidDataSource.init(DruidDataSource.java:669) INFO  - {dataSource-1} inited
2015-03-30 10:49:49,812 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'dataSource'<>
2015-03-30 10:49:49,836 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:23) INFO  - Init file-pool by: C:\Users\wendal/.nutz/tmp/dao/ [200000]
2015-03-30 10:49:49,837 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:37) DEBUG - file-pool.home: 'C:\Users\wendal\.nutz\tmp\dao'
2015-03-30 10:49:49,843 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:66) INFO  - file-pool.cursor: 120
2015-03-30 10:49:49,848 org.nutz.dao.jdbc.Jdbcs.<clinit>(Jdbcs.java:85) DEBUG - Jdbcs init complete
2015-03-30 10:49:49,849 org.nutz.dao.jdbc.Jdbcs.getExpert(Jdbcs.java:98) INFO  - Get Connection from DataSource for JdbcExpert
2015-03-30 10:49:50,062 org.nutz.dao.impl.DaoSupport$1.invoke(DaoSupport.java:165) DEBUG - JDBC Driver --> mysql-connector-java-5.1.34 ( Revision: jess.balint@oracle.com-20141014163213-wqbwpf1ok2kvo1om )
2015-03-30 10:49:50,063 org.nutz.dao.impl.DaoSupport$1.invoke(DaoSupport.java:166) DEBUG - JDBC Name   --> MySQL Connector Java
2015-03-30 10:49:50,063 org.nutz.dao.impl.DaoSupport.setDataSource(DaoSupport.java:174) DEBUG - Database info --> MYSQL:[MySQL - 5.5.5-10.1.2-MariaDB]
2015-03-30 10:49:50,070 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-03-30 10:49:50,120 org.nutz.dao.impl.sql.run.NutDaoExecutor._runSelect(NutDaoExecutor.java:193) DEBUG - SELECT COUNT(*) FROM t_user 
2015-03-30 10:49:50,121 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:126) INFO  - Nutz.Mvc[nutz] is up in 593ms
```

## 启动日志的顺序

* 输出日志系统将通过什么接口输出,内置2种实现都会输出提示
	* System.out或System.err
	* Log4j
* Nutz版权声明及反馈地址
* NutFilter启动
* 资源扫描器开始初始化
* NutFilter输出容器信息
* 加载MainModule
* 加载Ioc配置信息
* 解析路径映射的信息
* 执行用户自定义Setup的信息
* NutFilter完成的耗时信息