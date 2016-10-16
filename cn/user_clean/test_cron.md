# 检查效果

## 启动Tomcat, 应该能看到类似的log信息

```
2015-04-14 22:33:19,945 net.wendal.nutzbook.quartz.NutQuartzCronJobFactory.init(NutQuartzCronJobFactory.java:33) DEBUG - job define name=CleanNonActiveUserJob cron=0 0/2 * * * ?
```

及启动Job之后的输出

```

2015-04-14 22:36:00,001 org.quartz.core.JobRunShell.run(JobRunShell.java:201) DEBUG - Calling execute on job DEFAULT.6da64b5bd2ee-3a6662c5-ef40-44ca-8794-7cc89966c3e9
2015-04-14 22:36:00,001 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:28) DEBUG - clean Non-Active User , start
2015-04-14 22:36:00,002 org.nutz.dao.impl.sql.run.NutDaoExecutor._runPreparedStatement(NutDaoExecutor.java:255) DEBUG - DELETE FROM t_user_profile WHERE uid>? AND ct<? AND (email_checked=? OR email IS NULL )
    |  1 |          2 |     3 |
    |----|------------|-------|
    | 10 | 2015-04-13 | false |
  For example:> "DELETE FROM t_user_profile WHERE uid>10 AND ct<'2015-04-13' AND (email_checked=false OR email IS NULL )"
2015-04-14 22:36:00,004 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:32) DEBUG - delete 0 UserProfile
2015-04-14 22:36:00,004 org.nutz.dao.impl.sql.run.NutDaoExecutor._runStatement(NutDaoExecutor.java:313) DEBUG - delete from t_user where id > 10 and not exists (select 1 from t_user_profile UP where t_user.id = uid )
2015-04-14 22:36:00,008 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:39) DEBUG - clean Non-Active User , Done
```

## 现在登录,并打开用户列表页

```
http://127.0.0.1:8080/nutzbook/user/
```

### 请狠狠地添加几个用户,并确保最后一个用户的id在10以上

## 默默等待一天... 或者,改一下CleanNonActiveUserJob里面的超时设置(记得还原啊),并重启Tomcat.

```
2015-04-14 23:10:00,000 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'cleanNonActiveUserJob'<class net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob>
2015-04-14 23:10:00,001 org.quartz.core.QuartzSchedulerThread.run(QuartzSchedulerThread.java:276) DEBUG - batch acquisition of 0 triggers
2015-04-14 23:10:00,001 org.quartz.core.JobRunShell.run(JobRunShell.java:201) DEBUG - Calling execute on job DEFAULT.6da64b5bd2ee-23824fd7-b664-4bdd-9c95-956215902e85
2015-04-14 23:10:00,001 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:28) DEBUG - clean Non-Active User , start
2015-04-14 23:10:00,002 org.nutz.dao.impl.sql.run.NutDaoExecutor._runPreparedStatement(NutDaoExecutor.java:255) DEBUG - DELETE FROM t_user_profile WHERE uid>? AND ct<? AND (email_checked=? OR email IS NULL )
    |  1 |                   2 |     3 |
    |----|---------------------|-------|
    | 10 | 2015-04-14 23:05:00 | false |
  For example:> "DELETE FROM t_user_profile WHERE uid>10 AND ct<'2015-04-14 23:05:00' AND (email_checked=false OR email IS NULL )"
2015-04-14 23:10:00,003 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:32) DEBUG - delete 0 UserProfile
2015-04-14 23:10:00,004 org.nutz.dao.impl.sql.run.NutDaoExecutor._runPreparedStatement(NutDaoExecutor.java:255) DEBUG - delete from t_user where id > 10 and not exists (select 1 from t_user_profile where t_user.id = uid ) and ct < '2015-04-14 23:05:00'
2015-04-14 23:10:00,008 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:39) DEBUG - delete 1 User
2015-04-14 23:10:00,008 net.wendal.nutzbook.quartz.job.CleanNonActiveUserJob.execute(CleanNonActiveUserJob.java:41) DEBUG - clean Non-Active User , Done

```

### 看到 delete 1 User 之类的,就胜利了.

### 如果你发现一直没有输出,请打开UserModule的add方法,在insert之前加上

```java
		user.setCreateTime(new Date());
		user.setUpdateTime(new Date());
```

### 我也是写着写着才发现这个问题...