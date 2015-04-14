# 添加cron任务加载类

## 首先,新建一个配置文件 conf/custom/cron.properties

```ini
# clean non-active user
cron.CleanNonActiveUserJob=0 0/2 * * * ?
```

### 这个文件是定义Job类与cron表达式的关系,格式是

* 所有属性cron.开头
* cron.XXX 其中的XXX是类全名或者是简单类名(在加载器中自动补齐package)
* 等号的另外一侧是cron表达式, 从左到右分别是 秒 分 时 日 月 星期 年
* 这里的cron表达式含义是每2分钟检查一次(按时钟算),是比较频繁,测试ok后将改成1小时一次甚至更久.


## 再建一个 net.wendal.nutzbook.quartz.NutQuartzCronJobFactory, 这个类的作用是读取cron.properties里面的配置,然后启动相应的计划任务

```
package net.wendal.nutzbook.quartz;

import org.nutz.ioc.impl.PropertiesProxy;
import org.nutz.ioc.loader.annotation.Inject;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.log.Log;
import org.nutz.log.Logs;
import org.quartz.CronScheduleBuilder;
import org.quartz.CronTrigger;
import org.quartz.Job;
import org.quartz.JobBuilder;
import org.quartz.JobDetail;
import org.quartz.Scheduler;
import org.quartz.TriggerBuilder;

@IocBean(create="init")
public class NutQuartzCronJobFactory {
	
	private static final Log log = Logs.get();

	@Inject protected PropertiesProxy conf;
	
	@Inject protected Scheduler scheduler;
	
	@SuppressWarnings("unchecked")
	public void init() throws Exception {
		String prefix = "cron.";
		for (String key : conf.getKeys()) {
			if (key.length() < prefix.length()+1 || !key.startsWith(prefix))
				continue;
			String name = key.substring(prefix.length());
			String cron = conf.get(key);
			log.debugf("job define name=%s cron=%s", name, cron);
			Class<?> klass = null;
			if (name.contains(".")) {
				klass = Class.forName(name);
			} else {
				klass = Class.forName(getClass().getPackage().getName() + ".job." + name);
			}
			JobDetail job = JobBuilder.newJob((Class<? extends Job>) klass).build();
			CronTrigger trigger = TriggerBuilder.newTrigger().withIdentity(name)
				    .withSchedule(CronScheduleBuilder.cronSchedule(cron))
				    .build();
			scheduler.scheduleJob(job, trigger);
		}
	}

}
```

### 关键点

* 其中的PropertiesProxy conf是指向的是dao.js中的conf配置, 因为cron.properties也在custom目录下,所以可以一并读取到
* 这里注入了Scheduler,所以加载这个类时quartz也启动了
* 代码中name, 带点号的将归于完整类名,否则就是类短名.
* 综上条件, 下面我们将会新建一个叫net.wendal.nutzbook.quartz.CleanNonActiveUserJob的类.