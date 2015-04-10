# 加入Quartz

## 把下列的jar放入WebContent/WEB-INF/lib下

* quartz-2.2.1.jar
* quartz-jobs-2.2.1.jar

## 在conf目录下,新建一个文件叫quartz.properties,内容如下

```java
org.quartz.scheduler.instanceName = NutzbookScheduler 
org.quartz.threadPool.threadCount = 3 
org.quartz.jobStore.class = org.quartz.simpl.RAMJobStore
org.quartz.scheduler.skipUpdateCheck=true
```

## 新建一个类, 包为net.wendal.nutzbook.quartz, 名称为NutQuartzJobFactory, 内容如下

```java
package net.wendal.nutzbook.quartz;

import org.nutz.ioc.Ioc;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.log.Log;
import org.nutz.log.Logs;
import org.quartz.Job;
import org.quartz.Scheduler;
import org.quartz.SchedulerException;
import org.quartz.simpl.SimpleJobFactory;
import org.quartz.spi.JobFactory;
import org.quartz.spi.TriggerFiredBundle;

@IocBean(args="refer:$ioc")
public class NutQuartzJobFactory implements JobFactory {

	private static final Log log = Logs.get();

	protected SimpleJobFactory simple = new SimpleJobFactory();

	protected Ioc ioc;
	
	public NutQuartzJobFactory(Ioc ioc) {
		this.ioc = ioc;
	}

	public Job newJob(TriggerFiredBundle bundle, Scheduler scheduler) throws SchedulerException {
		try {
			return ioc.get(bundle.getJobDetail().getJobClass());
		}
		catch (Exception e) {
			log.warn("Not ioc bean? fallback to SimpleJobFactory", e);
			return simple.newJob(bundle, scheduler);
		}
	}

}
```

## 打开MainSetup类,在创建用户之后,加入一行代码

```java
		// 获取quartz的Scheduler,这样就自动触发了计划任务的启动
		ioc.get(Scheduler.class);
```

其中的Scheduler是org.quartz.Scheduler

## 在conf/ioc目录下,创建一个文件quartz.js 内容如下

```js
var ioc = {
		scheduler : {
			type : "org.quartz.Scheduler",
			factory: "org.quartz.impl.StdSchedulerFactory#getDefaultScheduler",
			events : {
				create : "start",
				depose : "shutdown",
			},
			fields : {
				jobFactory : {refer:"nutQuartzJobFactory"}
			}
		}
};
```

## 仔细检查后,启动tomcat, 应有如下log输出

```
2015-04-09 20:29:03,691 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'scheduler'<interface org.quartz.Scheduler>
2015-04-09 20:29:03,691 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:166) DEBUG - 	 >> Load definition
2015-04-09 20:29:03,691 org.nutz.ioc.loader.map.MapLoader.load(MapLoader.java:67) DEBUG - Loading define for name=scheduler
2015-04-09 20:29:03,691 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:137) DEBUG - Found IocObject(scheduler) in IocLoader(JsonLoader@2112201553)
2015-04-09 20:29:03,691 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'scheduler'<interface org.quartz.Scheduler>
2015-04-09 20:29:03,697 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:82) DEBUG - interface org.quartz.Scheduler , no config to enable AOP for this type.
2015-04-09 20:29:03,698 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'scheduler' to [app] 
2015-04-09 20:29:03,724 org.quartz.impl.StdSchedulerFactory.instantiate(StdSchedulerFactory.java:1184) INFO  - Using default implementation for ThreadExecutor
2015-04-09 20:29:03,739 org.quartz.core.SchedulerSignalerImpl.<init>(SchedulerSignalerImpl.java:61) INFO  - Initialized Scheduler Signaller of type: class org.quartz.core.SchedulerSignalerImpl
2015-04-09 20:29:03,739 org.quartz.core.QuartzScheduler.<init>(QuartzScheduler.java:240) INFO  - Quartz Scheduler v.2.2.1 created.
2015-04-09 20:29:03,740 org.quartz.simpl.RAMJobStore.initialize(RAMJobStore.java:155) INFO  - RAMJobStore initialized.
2015-04-09 20:29:03,740 org.quartz.core.QuartzScheduler.initialize(QuartzScheduler.java:305) INFO  - Scheduler meta-data: Quartz Scheduler (v2.2.1) 'NutzbookScheduler' with instanceId 'NON_CLUSTERED'
  Scheduler class: 'org.quartz.core.QuartzScheduler' - running locally.
  NOT STARTED.
  Currently in standby mode.
  Number of jobs executed: 0
  Using thread pool 'org.quartz.simpl.SimpleThreadPool' - with 3 threads.
  Using job-store 'org.quartz.simpl.RAMJobStore' - which does not support persistence. and is not clustered.

2015-04-09 20:29:03,740 org.quartz.impl.StdSchedulerFactory.instantiate(StdSchedulerFactory.java:1339) INFO  - Quartz scheduler 'NutzbookScheduler' initialized from default resource file in Quartz package: 'quartz.properties'
2015-04-09 20:29:03,741 org.quartz.impl.StdSchedulerFactory.instantiate(StdSchedulerFactory.java:1343) INFO  - Quartz scheduler version: 2.2.1
2015-04-09 20:29:03,741 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'nutQuartzJobFactory'<>
2015-04-09 20:29:03,741 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:166) DEBUG - 	 >> Load definition
2015-04-09 20:29:03,741 org.nutz.ioc.loader.combo.ComboIocLoader.load(ComboIocLoader.java:137) DEBUG - Found IocObject(nutQuartzJobFactory) in IocLoader(AnnotationIocLoader@394683855)
2015-04-09 20:29:03,741 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:193) DEBUG - 	 >> Make...'nutQuartzJobFactory'<>
2015-04-09 20:29:03,741 org.nutz.ioc.aop.impl.DefaultMirrorFactory.getMirror(DefaultMirrorFactory.java:82) DEBUG - class net.wendal.nutzbook.quartz.NutQuartzJobFactory , no config to enable AOP for this type.
2015-04-09 20:29:03,741 org.nutz.ioc.impl.ScopeContext.save(ScopeContext.java:59) DEBUG - Save object 'nutQuartzJobFactory' to [app] 
2015-04-09 20:29:03,742 org.quartz.core.QuartzScheduler.setJobFactory(QuartzScheduler.java:2311) INFO  - JobFactory set to: net.wendal.nutzbook.quartz.NutQuartzJobFactory@6e8b5c48
2015-04-09 20:29:03,742 org.quartz.core.QuartzScheduler.start(QuartzScheduler.java:575) INFO  - Scheduler NutzbookScheduler_$_NON_CLUSTERED started.
2015-04-09 20:29:03,742 org.quartz.core.QuartzSchedulerThread.run(QuartzSchedulerThread.java:276) DEBUG - batch acquisition of 0 triggers
```

代表各种初始化操作.