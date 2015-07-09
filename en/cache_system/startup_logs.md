# 启动Tomcat观察日志

这一章并没有修改页面,但启动tomcat后,登陆完成后,进入用户详情页,清空日志,然后刷新页面,你就能看到并无sql查询的痕迹

日志类似于
---------------------

```log
2015-05-22 10:37:59,799 org.nutz.mvc.impl.UrlMappingImpl.get(UrlMappingImpl.java:92) DEBUG - Found mapping for [GET] path=/home : PageModule.home(...)
2015-05-22 10:37:59,799 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'pageModule'<class net.wendal.nutzbook.module.PageModule>
2015-05-22 10:37:59,808 net.wendal.nutzbook.mvc.LogTimeProcessor.process(LogTimeProcessor.java:27) DEBUG - [GET ]URI=/nutzbook/home 8ms
2015-05-22 10:37:59,882 org.nutz.mvc.impl.UrlMappingImpl.get(UrlMappingImpl.java:92) DEBUG - Found mapping for [GET] path=/user/profile/avatar : UserProfileModule.readAvatar(...)
2015-05-22 10:37:59,882 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'userProfileModule'<class net.wendal.nutzbook.module.UserProfileModule>
2015-05-22 10:37:59,884 net.wendal.nutzbook.mvc.LogTimeProcessor.process(LogTimeProcessor.java:27) DEBUG - [GET ]URI=/nutzbook/user/profile/avatar 2ms
2015-05-22 10:37:59,917 org.nutz.mvc.impl.UrlMappingImpl.get(UrlMappingImpl.java:92) DEBUG - Found mapping for [GET] path=/user/profile/get : UserProfileModule.get(...)
2015-05-22 10:37:59,917 org.nutz.ioc.impl.NutIoc.get(NutIoc.java:144) DEBUG - Get 'userProfileModule'<class net.wendal.nutzbook.module.UserProfileModule>
2015-05-22 10:37:59,920 net.wendal.nutzbook.mvc.LogTimeProcessor.process(LogTimeProcessor.java:27) DEBUG - [GET ]URI=/nutzbook/user/profile/get 3ms

```

如果你需要详细的缓存日志,在MainSetup的init方法加入下面的代码
----------------------------------

```java
CachedNutDaoExecutor.DEBUG = true;
```