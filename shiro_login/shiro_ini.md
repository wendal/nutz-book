# 修改shiro.ini

## shiro.ini的内容终于有实际含义了

```ini
[main]
sha256Matcher = org.apache.shiro.authc.credential.Sha256CredentialsMatcher
nutzdao_realm = net.wendal.nutzbook.shiro.realm.NutDaoRealm
nutzdao_realm.credentialsMatcher = $sha256Matcher

authc = org.nutz.integration.shiro.CaptchaFormAuthenticationFilter
authc.loginUrl  = /user/login
logout.redirectUrl= /user/login

[urls]
/rs/*        = anon
/user/logout = logout
/user/error  = anon
/user/profile/active/mail = anon
/user/**     = authc
```

### 看这里看这里

* main节点的sha256Matcher与UserService里面的密码加密算法是强相关的,修改这里的值,必须同步修改UserService的实现
* CaptchaFormAuthenticationFilter取之于rk_cms项目, 改造并存在于shiro插件中
* /user/login是UserModule的login方法所映射的路径, 这里的配置将会拦截之,所以可以通过日志的输出看到是否真的使用了shiro登陆
* nutzdao_realm指向的就是前一小节新增的NutDaoRealm