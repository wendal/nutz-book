# URL映射关系的Log

## 这个log比较多

```

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
```

## 来研究研究一下这堆log

* 第一条, 显示MainModule所在的实际路径, 这是解决Maven下的扫描出错的bug的日志
* 第二条, 显示正在扫描的package的路径
* 第三条, 资源扫描的log, 均为MainModule中```@Modules(scanPackage=true)```所触发的扫描行为. 这里供得到4个类,但不等于就是4个模块, 带```@At```入口方法的类,才会成为模块类
* 第四条开始, 就是各入口方法的信息了, 现在挑第一条进行完整讲解
	* ``` '/user/' ```是映射的完整的路径. 类路径+方法路径
	* ``` void ``` 入口方法的返回值类型. 如果你配置了@Ok("json")然后返回值是String,它就是警告你.
	* ```UserModule.index(...)``` 映射的类名及方法名
	* ```@Ok(jsp:jsp.user.list)``` @Ok的配置,这里的含义是jsp视图的jsp.user.list路径.
	* ```@Fail(http:500)``` @Fail的配置,这是入口方法或适配器抛出异常才会执行的配置
	* ```by 1 Filters``` @Filters的配置,这里并不会给出完整的,不然真的很长很长. 请留意一下login方法时0个Filters.
	* ```(I:UTF-8/O:UTF-8)``` 最后是编码设置,影响的是POST时的body编码,注意啊,URL的编码是不会受影响的,那不是Servlet API标准里面可以设置的内容.

## 入口方法的各种配置的优先顺序

* 第一原则, 不可叠加的注解, 例如Ok,Fail,Filters, 优先级是 入口方法>类>MainModule
* 可叠加的注解,其实只有At, 优先级是 入口方法+(类>MainModule)