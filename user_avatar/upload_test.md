# 页面测试

## 启动Tomcat, 观察log输出

* 有建表的Log(加UserProfile类之后的第一次启动会有)
* URL映射的Log输出了/usr/profile相关的路径
* Upload方法的临时文件池的初始化log

```
2015-04-13 10:40:26,299 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:23) INFO  - Init file-pool by: D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook/WEB-INF/tmp/user_avatar [20000]
2015-04-13 10:40:26,301 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:37) DEBUG - file-pool.home: 'D:\nutzbook\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\nutzbook\WEB-INF\tmp\user_avatar'
2015-04-13 10:40:26,304 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:66) INFO  - file-pool.cursor: 28
```

## 访问首页,进行登录

```
http://127.0.0.1:8080/nutzbook/
```

## 访问详情页

```
http://127.0.0.1:8080/nutzbook/user/profile/
```

![](images/profile_page.png)

## 填入昵称,邮箱等,点击下方的更新, 页面应自动刷新, 看后台的log输出

```
2015-04-13 10:44:19,305 org.nutz.mvc.impl.UrlMappingImpl.get(UrlMappingImpl.java:92) DEBUG - Found mapping for [POST] path=/user/profile/update : UserProfileModule.update(...)
2015-04-13 10:44:19,306 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'userProfileModule'<class net.wendal.nutzbook.module.UserProfileModule>
2015-04-13 10:44:19,308 org.nutz.dao.impl.sql.run.NutDaoExecutor._runSelect(NutDaoExecutor.java:212) DEBUG - SELECT uid,nickname,email,email_checked,gender,dt,loc,ct,ut FROM t_user_profile  WHERE uid=?
    | 1 |
    |---|
    | 1 |
  For example:> "SELECT uid,nickname,email,email_checked,gender,dt,loc,ct,ut FROM t_user_profile  WHERE uid=1"
2015-04-13 10:44:19,315 org.nutz.dao.impl.sql.run.NutDaoExecutor._runPreparedStatement(NutDaoExecutor.java:255) DEBUG - UPDATE t_user_profile SET nickname=?,email=?,email_checked=?,gender=?,dt=?,loc=?,ut=?  WHERE uid=?
    |        1 |            2 |     3 | 4 |       5 |  6 |                   7 | 8 |
    |----------|--------------|-------|---|---------|----|---------------------|---|
    | wendalsf | vt400@qq.com | false | m | 阿斯顿发斯蒂芬 | 地球 | 2015-04-13 10:44:19 | 1 |
  For example:> "UPDATE t_user_profile SET nickname='wendalsf',email='vt400@qq.com',email_checked=false,gender='m',dt='阿斯顿发斯蒂芬',loc='地球',ut='2015-04-13 10:44:19'  WHERE uid=1"
2015-04-13 10:44:19,323 net.wendal.nutzbook.mvc.LogTimeProcessor.process(LogTimeProcessor.java:27) DEBUG - [POST]URI=/nutzbook/user/profile/update 17ms
```

## 点击"选择文件", 挑一张你喜欢的图片(小于100kb),然后点击更新头像

* 页面应立即刷新, 本地操作嘛
* 头像从默认头像变成刚刚上传的图片

## 可能出现的问题

* jsp错误, 有可能是UserProfile的字段写错
* 数据库错误, 检查UserProfile的字段是否写全,如果不行可以删除数据库表,然后重启应用.