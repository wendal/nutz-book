# 页面测试

## 一切就绪,请再仔细检查一下本章的修改,然后启动Tomcat, 首先的输出的日志将会发生变化

```
2015-04-17 12:35:54,625 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) DEBUG - Creating instance from Ini [sections=main,urls]
2015-04-17 12:35:54,688 org.apache.shiro.config.ReflectionBuilder.createNewInstance(ReflectionBuilder.java:138) INFO  - An instance with name 'authc' already exists.  Redefining this object as a new instance of type org.nutz.integration.shiro.CaptchaFormAuthenticationFilter
2015-04-17 12:35:54,767 org.apache.shiro.config.ReflectionBuilder.resolveReference(ReflectionBuilder.java:238) DEBUG - Encountered object reference '$sha256Matcher'.  Looking up object with id 'sha256Matcher'
2015-04-17 12:35:54,801 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:234) DEBUG - No authorizationCache instance set.  Checking for a cacheManager...
2015-04-17 12:35:54,801 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:248) INFO  - No cache or cacheManager properties have been set.  Authorization cache cannot be obtained.
2015-04-17 12:35:54,804 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) DEBUG - Creating instance from Ini [sections=main,urls]
2015-04-17 12:35:54,808 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) DEBUG - Creating chain [/rs/*] from String definition [anon]
2015-04-17 12:35:54,808 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) DEBUG - Attempting to apply path [/rs/*] to filter [anon] with config [null]
2015-04-17 12:35:54,810 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) DEBUG - Creating chain [/user/logout] from String definition [logout]
2015-04-17 12:35:54,811 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) DEBUG - Attempting to apply path [/user/logout] to filter [logout] with config [null]
2015-04-17 12:35:54,811 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) DEBUG - Creating chain [/user/error] from String definition [anon]
2015-04-17 12:35:54,812 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) DEBUG - Attempting to apply path [/user/error] to filter [anon] with config [null]
2015-04-17 12:35:54,812 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) DEBUG - Creating chain [/user/**] from String definition [authc]
2015-04-17 12:35:54,812 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) DEBUG - Attempting to apply path [/user/**] to filter [authc] with config [null]
2015-04-17 12:35:54,812 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:136) DEBUG - Published WebEnvironment as ServletContext attribute with name [org.apache.shiro.web.env.EnvironmentLoader.ENVIRONMENT_ATTRIBUTE_KEY]
2015-04-17 12:35:54,812 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:141) INFO  - Shiro environment initialized in 221 ms.
```

### 请留意其中的sha256Matcher, CaptchaFormAuthenticationFilter资源,确保都是正确的,无异常的.

## 访问新的登陆页面

```
http://127.0.0.1:8080/nutzbook/user/logout
```

### 应该自动跳到如下地址

```
http://127.0.0.1:8080/nutzbook/user/login
```

### 如果出现404或者跳到根路径,检查日志中是否有shiro的输出, 检查shiro.ini的配置

## 登陆应无障碍, 登陆成功后进入用户详情页

## 访问用户列表页, 尝试新增几个用户,然后登出,用新账号登陆


```
http://127.0.0.1:8080/nutzbook/user/
```

登出

```
http://127.0.0.1:8080/nutzbook/user/login
```

