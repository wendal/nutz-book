# 页面测试

## 一切就绪,请再仔细检查一下本章的修改,然后启动Tomcat, 首先的输出的日志将会发生变化

```
[INFO ] 20:33:09.574 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:128) - Starting Shiro environment initialization.
[DEBUG] 20:33:09.594 org.apache.shiro.web.env.IniWebEnvironment.init(IniWebEnvironment.java:76) - Checking any specified config locations.
[DEBUG] 20:33:09.594 org.apache.shiro.web.env.IniWebEnvironment.init(IniWebEnvironment.java:81) - No INI instance or config locations specified.  Trying default config locations.
[DEBUG] 20:33:09.602 org.apache.shiro.io.ResourceUtils.loadFromClassPath(ResourceUtils.java:159) - Opening resource from class path [shiro.ini]
[DEBUG] 20:33:09.607 org.apache.shiro.config.Ini.load(Ini.java:351) - Parsing [main]
[DEBUG] 20:33:09.610 org.apache.shiro.config.Ini.load(Ini.java:351) - Parsing [urls]
[DEBUG] 20:33:09.611 org.apache.shiro.web.env.IniWebEnvironment.getDefaultIni(IniWebEnvironment.java:136) - Discovered non-empty INI configuration at location 'classpath:shiro.ini'.  Using for configuration.
[DEBUG] 20:33:09.616 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) - Creating instance from Ini [sections=main,urls]
[DEBUG] 20:33:10.040 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:234) - No authorizationCache instance set.  Checking for a cacheManager...
[DEBUG] 20:33:10.040 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:248) - No cache or cacheManager properties have been set.  Authorization cache cannot be obtained.
[INFO ] 20:33:10.041 org.apache.shiro.config.ReflectionBuilder.createNewInstance(ReflectionBuilder.java:296) - An instance with name 'authc' already exists.  Redefining this object as a new instance of type org.nutz.integration.shiro.SimpleAuthenticationFilter
[DEBUG] 20:33:10.121 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:234) - No authorizationCache instance set.  Checking for a cacheManager...
[DEBUG] 20:33:10.122 org.apache.shiro.realm.AuthorizingRealm.getAuthorizationCacheLazy(AuthorizingRealm.java:248) - No cache or cacheManager properties have been set.  Authorization cache cannot be obtained.
[DEBUG] 20:33:10.125 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) - Creating instance from Ini [sections=main,urls]
[DEBUG] 20:33:10.128 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/rs/*] from String definition [anon, noSessionCreation]
[DEBUG] 20:33:10.129 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/rs/*] to filter [anon] with config [null]
[DEBUG] 20:33:10.130 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/rs/*] to filter [noSessionCreation] with config [null]
[DEBUG] 20:33:10.130 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/druid/*] from String definition [anon, noSessionCreation]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/druid/*] to filter [anon] with config [null]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/druid/*] to filter [noSessionCreation] with config [null]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/asserts/*] from String definition [anon, noSessionCreation]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/asserts/*] to filter [anon] with config [null]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/asserts/*] to filter [noSessionCreation] with config [null]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/user/logout] from String definition [logout]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/user/logout] to filter [logout] with config [null]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/user/error] from String definition [anon]
[DEBUG] 20:33:10.131 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/user/error] to filter [anon] with config [null]
[DEBUG] 20:33:10.132 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) - Creating chain [/user/profile/active/mail] from String definition [anon]
[DEBUG] 20:33:10.132 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) - Attempting to apply path [/user/profile/active/mail] to filter [anon] with config [null]
[DEBUG] 20:33:10.132 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:136) - Published WebEnvironment as ServletContext attribute with name [org.apache.shiro.web.env.EnvironmentLoader.ENVIRONMENT_ATTRIBUTE_KEY]
[INFO ] 20:33:10.132 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:141) - Shiro environment initialized in 555 ms.
```

### 请留意其中的SimpleAuthenticationFilter,确保都是正确的,无异常的.

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

