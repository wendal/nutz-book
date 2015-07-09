# 加入Quartz

## 把下列的jar放入WebContent/WEB-INF/lib下

* quartz-2.2.1.jar
* quartz-jobs-2.2.1.jar
* nutz-integration-quartz-1.b.52.jar

## 在conf目录下,新建一个文件叫quartz.properties,内容如下

```java
org.quartz.scheduler.instanceName = NutzbookScheduler 
org.quartz.threadPool.threadCount = 3 
org.quartz.jobStore.class = org.quartz.simpl.RAMJobStore
org.quartz.scheduler.skipUpdateCheck=true
```

## 打开MainModule,修改IocBy为

```java
@IocBy(type=ComboIocProvider.class, args={"*js", "ioc/",
										   "*anno", "net.wendal.nutzbook",
										   "*tx",
										   "*org.nutz.integration.quartz.QuartzIocLoader"})
```

### 即添加了 org.nutz.integration.quartz.QuartzIocLoader 这个预定义的集成配置

## 打开MainSetup类, 在init方法末尾,添加代码

```
		// 获取NutQuartzCronJobFactory从而触发计划任务的初始化与启动
		ioc.get(NutQuartzCronJobFactory.class);
```


## 仔细检查后,启动tomcat, 应有如下log输出

```
2015-04-24 23:07:34,706 org.quartz.core.SchedulerSignalerImpl.<init>(SchedulerSignalerImpl.java:61) INFO  - Initialized Scheduler Signaller of type: class org.quartz.core.SchedulerSignalerImpl
2015-04-24 23:07:34,706 org.quartz.core.QuartzScheduler.<init>(QuartzScheduler.java:240) INFO  - Quartz Scheduler v.2.2.1 created.
2015-04-24 23:07:34,707 org.quartz.simpl.RAMJobStore.initialize(RAMJobStore.java:155) INFO  - RAMJobStore initialized.
2015-04-24 23:07:34,707 org.quartz.core.QuartzScheduler.initialize(QuartzScheduler.java:305) INFO  - Scheduler meta-data: Quartz Scheduler (v2.2.1) 'NutzbookScheduler' with instanceId 'NON_CLUSTERED'
  Scheduler class: 'org.quartz.core.QuartzScheduler' - running locally.
  NOT STARTED.
  Currently in standby mode.
  Number of jobs executed: 0
  Using thread pool 'org.quartz.simpl.SimpleThreadPool' - with 3 threads.
  Using job-store 'org.quartz.simpl.RAMJobStore' - which does not support persistence. and is not clustered.

2015-04-24 23:07:34,708 org.quartz.impl.StdSchedulerFactory.instantiate(StdSchedulerFactory.java:1339) INFO  - Quartz scheduler 'NutzbookScheduler' initialized from default resource file in Quartz package: 'quartz.properties'
2015-04-24 23:07:34,708 org.quartz.impl.StdSchedulerFactory.instantiate(StdSchedulerFactory.java:1343) INFO  - Quartz scheduler version: 2.2.1
2015-04-24 23:07:34,708 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'jobFactory'<>
2015-04-24 23:07:34,708 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:166) DEBUG - 	 >> Load definition
2015-04-24 23:07:34,708 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=jobFactory
2015-04-24 23:07:34,709 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:137) DEBUG - Found IocObject(jobFactory) in IocLoader(QuartzIocLoader@1177174666)
2015-04-24 23:07:34,709 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'jobFactory'<>
2015-04-24 23:07:34,710 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:82) DEBUG - class org.nutz.integration.quartz.NutQuartzJobFactory , no config to enable AOP for this type.
2015-04-24 23:07:34,710 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'jobFactory' to [app] 
2015-04-24 23:07:34,711 org.quartz.core.QuartzScheduler.setJobFactory(QuartzScheduler.java:2311) INFO  - JobFactory set to: org.nutz.integration.quartz.NutQuartzJobFactory@48de4231
2015-04-24 23:07:34,711 org.quartz.core.QuartzScheduler.start(QuartzScheduler.java:575) INFO  - Scheduler NutzbookScheduler_$_NON_CLUSTERED started.
```

代表各种初始化操作.