# 启动并观察日志

请再次检查所有的RequiresPermissions注解是否正常,然后启动Tomcat
------------------------------------------------

如无意外,你将会看到类似的log

```
2015-05-21 21:30:34,594 net.wendal.nutzbook.service.AuthorityServiceImpl.initFormPackage(AuthorityServiceImpl.java:60) DEBUG - found 17 permission
2015-05-21 21:30:34,594 net.wendal.nutzbook.service.AuthorityServiceImpl.initFormPackage(AuthorityServiceImpl.java:61) DEBUG - found 0 role
```

即找到17个权限,然后就是插入到数据,关联admin角色等sql输出

测试一下效果
---------------------

先登录,然后访问

```
http://127.0.0.1:8080/nutzbook/page/simple_role.jsp
```

出现一个很神奇的界面

![权限管理首页](images/startup_1.png)

点击"用户权限一览", "角色一览", "权限一览", 均可切换到不同的div

现在点击一下"权限一览", 显示有2页,点击一下 页数输入框右侧的箭头,变成2,就会更新为第二页的数据

![权限管理首页](images/startup_2.png)

其他功能请逐一尝试一下吧 -- 为用户添加角色,特许权限, 为角色添加权限等等