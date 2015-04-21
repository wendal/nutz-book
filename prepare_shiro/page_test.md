# 页面测试

## 启动Tomcat, 如无异常, 应该能看到多个建表语句输出

```
2015-04-16 23:57:19,738 org.nutz.dao.impl.sql.run.NutDaoExecutor._runStatement(NutDaoExecutor.java:313) DEBUG - CREATE TABLE t_user(
id INT(32) AUTO_INCREMENT,
name VARCHAR(50) UNIQUE NOT NULL,
passwd VARCHAR(128),
salt VARCHAR(50),
locked BOOLEAN,
ct DATETIME,
ut DATETIME,
PRIMARY KEY (id)
) ENGINE=InnoDB CHARSET=utf8
```

## 访问首页,登陆之

```
http://127.0.0.1:8080/nutzbook/
```

## 访问用户列表页,并新增一个用户,为简单期间,建议密码用123456

```
http://127.0.0.1:8080/nutzbook/user/
```

## 退出登陆

```
http://127.0.0.1:8080/nutzbook/user/
```

## 用新用户名登陆,然后再用户列表页,修改自己的密码,然后再登出,再用新密码登陆

## 可能遇到的问题

* admin登陆失败, 删掉t_user表并重启tomcat
* admin登陆依然失败,检查MainSetup中的用户密码是否写错
* admin登陆死活失败,检查UserService的登陆方法,必要时debug之
* 新用户登陆失败, 检查UserModule的add方法是否写对了
* 新用户修改密码后登陆失败, 检查UserModule的update方法及UserService

