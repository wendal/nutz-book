# MainSetup中触发AuthorityService

打开MainSetup类,在init方法末尾添加如下代码
---------------------------------------

```java
AuthorityService as = ioc.get(AuthorityService.class);
as.initFormPackage("net.wendal.nutzbook");
as.checkBasicRoles(dao.fetch(User.class, "admin"));
```

以上代码就能在启动时扫描注解,初始化最基本的权限模型,即:

* 用户admin存在
* 角色admin存在
* 用户admin属于admin角色
* admin角色拥有所有user:和authority:开头的权限