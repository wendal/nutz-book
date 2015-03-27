# 运行起来

## 现在,启动tomcat!!

访问URL

```
http://127.0.0.1:8080/nutzbook/
```

应该是这样的画面

![](images/runit_1.png)

## 点击提交后

![](images/runit_2.png)

![](images/runit_3.png)

## 自动刷新页面后

![](images/runit_4.png)

## 点击logout,又返回首页

![](images/runit_1.png)

## 如果输错密码,则提示登录失败

![](images/runit_5.png)

## 可能出现的问题

* 404 首页出不来,看看index.jsp文件名是不是错了
* 登录总是失败, 访问一下 user/count方法看看用户数是多少
* 登出404,检查一下logout方法的名字是不是写错了

## 本章结束时的项目压缩包

[登入登出基础项目的压缩包](zip/nutzbook_login_logout.zip)

为减少体积,里面的jar已经删除,请自行补齐.

## 手册关联(选修)

无