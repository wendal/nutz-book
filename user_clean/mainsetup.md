# 在MainSetup中触发

## 万事俱备,只欠东风,因为NutIoc中的Bean是完全懒加载模式的,不获取就不生成,不初始化,所以,为了触发计划任务的加载,我们需要改动一下, 把原本的

```
		// 获取quartz的Scheduler,这样就自动触发了计划任务的启动
		ioc.get(Scheduler.class);
```

改成

```
		// 获取NutQuartzCronJobFactory从而触发计划任务的初始化与启动
		ioc.get(NutQuartzCronJobFactory.class);
```

### 请顺手按一下 ctrl+shift+o, 清理import语句.