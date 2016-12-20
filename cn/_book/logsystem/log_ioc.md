# Ioc初始化的Log

## Ioc初始化的log全部揪出来,哈哈

```
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
```

## 来,把它宰了

* 第一条, 输出IocBy的具体配置,根本就是完全重现实际配置
* 第二条, 是资源扫描的log,但同时也是```"*js","ioc/"``` 所对应的日志. 含义是在classpath下的ioc目录找到1个js/json文件
* 第三条, JsonLoader读取dao.js的前置输出, 如果js出错了,下一条log就会变成XXX的json报错信息
* 第四条, JsonLoader读取dao.js的后置输出, 解析完成后的, 读取到了2个ioc bean定义
* 第五条, 也是资源扫描的log,但同时也是```"*anno", "net.wendal.nutzbook"```所对应的日志, 含义是扫描net.wendal.nutzbook及子package的类
* 第六条, AnnotationIocLoader开始对扫描得到的类进行解析,寻找带@IocBean注解的类,这里就是找到的第一个类UserModule
* 第七条, AnnotationIocLoader结束处理的总结陈词, 说在N个根package中找到了M个注解ioc的定义.
* 最后一条, 看上去是JsonLoader的输出,实际上是```*tx```所对应的TransIocLoader的输出, TransIocLoader类代理了一个JsonLoader实例. 这个配置也把Aop事务的相关配置给加载了. 以前的做法是单独写个trans.js来声明.