# Ioc获取对象的Log

## 前面说了Ioc初始化的log,这里说的是Ioc.get产生的log, 也就是从Ioc容器获取bean的log

```
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
```

## 庖丁解牛

### 导致这些log的代码,其实就一句,在MainSetup里面.

```
Dao dao = ioc.get(Dao.class);
```

* 第一条, 这其实是@SetupBy的log, 正是我们之前写的MainSetup类里面调用了```ioc.get```
* 第二条, 这是ioc.get方法在打印方法参数,不要误会那是对应ioc bean的属性. 另外, NutIoc是认名称,不是认类型的,默认就是首字母小写之后的类名(如果没有@IocBean或@InjectName配置的话)
* 第三条, 开始载入配置, 前置log,事情还没发生的
* 第四条, MapLoader(JsonLoader的超类)中找到名为dao的配置
* 第五条, ComboIocLoader提示在JsonLoader中找到名为dao的配置了
* 第六条, 再输出一次修正后的参数, 因为没东西需要修正,所以还是原样输出
* 第七条, 是AOP的拦截点, 因为没有对应的匹配方法,所以不需要对这个类启用AOP,跳过生成子类
* 第八条, 把当前的dao这bean的对象提前放入NutIoc的上下文, 是为了解决构造方法注入的问题
* 第九条到最后, dao这个bean的配置中引用了dataSource, 所以,往下的log都是为了生成dataSource对应的对象