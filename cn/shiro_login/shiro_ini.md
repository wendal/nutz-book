# 修改shiro.ini

## shiro.ini的内容终于有实际含义了

```ini
[main]
nutzdao_realm = net.wendal.nutzbook.shiro.realm.SimpleAuthorizingRealm

authc = org.nutz.integration.shiro.SimpleAuthenticationFilter
authc.loginUrl  = /user/login
logout.redirectUrl= /user/login

[urls]
/rs/*        = anon
/user/logout = logout
/user/error  = anon
/user/login  = anon
/user/profile/active/mail = anon
/user/**     = authc
```

### 看这里看这里

* SimpleAuthenticationFilter 不处理登录操作,直接穿透的
* /user/login是UserModule的login方法所映射的路径
* nutzdao_realm指向的就是前一小节新增的NutDaoRealm