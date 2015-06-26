# 添加cron任务加载类

## 首先,新建一个配置文件 conf/custom/cron.properties

```ini
# clean non-active user
cron.net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob=0 0/2 * * * ?
```

### 这个文件是定义Job类与cron表达式的关系,格式是

* 所有属性cron.开头
* cron.XXX 其中的XXX是类全名
* 等号的另外一侧是cron表达式, 从左到右分别是 秒 分 时 日 月 星期 年
* 这里的cron表达式含义是每2分钟检查一次(按时钟算),是比较频繁,测试ok后将改成1小时一次甚至更久.

### 关键点

* 其中的PropertiesProxy conf是指向的是dao.js中的conf配置, 因为cron.properties也在custom目录下,所以可以一并读取到
* 这里注入了Scheduler,所以加载这个类时quartz也启动了
* 代码中name, 带点号的将归于完整类名,否则就是类短名.
* 综上条件, 下面我们将会新建一个叫net.wendal.nutzbook.quartz.CleanNonActiveUserJob的类.