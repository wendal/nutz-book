# 加入Shiro

## 首先,下面罗列的jar 放入 WebContent/WEB-INF/lib中

* shiro-all-1.2.3.jar
* slf4j-api-1.7.12.jar
* slf4j-log4j12-1.7.12.jar
* commons-beanutils-1.9.2.jar
* commons-logging-1.2.jar
* nutz-integration-shiro-1.b.52.jar

## 在conf目录下,建一个文件叫shiro.ini, 右键--open with--Text Editor, 内容如下

```ini
[main]

[urls]
/* = anon
```
## 打开web.xml, 加入以下配置在其他filter之前哦

```xml
	<listener>
		<listener-class>org.apache.shiro.web.env.EnvironmentLoaderListener</listener-class>
	</listener>
	<filter>
		<filter-name>ShiroFilter</filter-name>
		<filter-class>org.apache.shiro.web.servlet.ShiroFilter</filter-class>
	</filter>

	<filter-mapping>
		<filter-name>ShiroFilter</filter-name>
		<url-pattern>/*</url-pattern>
		<dispatcher>REQUEST</dispatcher>
		<dispatcher>FORWARD</dispatcher>
		<dispatcher>INCLUDE</dispatcher>
		<dispatcher>ERROR</dispatcher>
	</filter-mapping>
```

## 启动tomcat, 可以看到多输出了一些log,这些log比nutz早

```
2015-04-09 20:03:45,821 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:128) INFO  - Starting Shiro environment initialization.
2015-04-09 20:03:45,834 org.apache.shiro.web.env.IniWebEnvironment.init(IniWebEnvironment.java:76) DEBUG - Checking any specified config locations.
2015-04-09 20:03:45,834 org.apache.shiro.web.env.IniWebEnvironment.init(IniWebEnvironment.java:81) DEBUG - No INI instance or config locations specified.  Trying default config locations.
2015-04-09 20:03:45,839 org.apache.shiro.io.ResourceUtils.loadFromClassPath(ResourceUtils.java:159) DEBUG - Opening resource from class path [shiro.ini]
2015-04-09 20:03:45,846 org.apache.shiro.config.Ini.load(Ini.java:342) DEBUG - Parsing [main]
2015-04-09 20:03:45,846 org.apache.shiro.config.Ini.load(Ini.java:342) DEBUG - Parsing [urls]
2015-04-09 20:03:45,848 org.apache.shiro.web.env.IniWebEnvironment.getDefaultIni(IniWebEnvironment.java:136) DEBUG - Discovered non-empty INI configuration at location 'classpath:shiro.ini'.  Using for configuration.
2015-04-09 20:03:45,850 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) DEBUG - Creating instance from Ini [sections=urls]
2015-04-09 20:03:45,897 org.apache.shiro.config.IniFactorySupport.createInstance(IniFactorySupport.java:122) DEBUG - Creating instance from Ini [sections=urls]
2015-04-09 20:03:45,901 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.createChain(DefaultFilterChainManager.java:127) DEBUG - Creating chain [/*] from String definition [anon]
2015-04-09 20:03:45,902 org.apache.shiro.web.filter.mgt.DefaultFilterChainManager.applyChainConfig(DefaultFilterChainManager.java:278) DEBUG - Attempting to apply path [/*] to filter [anon] with config [null]
2015-04-09 20:03:45,903 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:136) DEBUG - Published WebEnvironment as ServletContext attribute with name [org.apache.shiro.web.env.EnvironmentLoader.ENVIRONMENT_ATTRIBUTE_KEY]
2015-04-09 20:03:45,903 org.apache.shiro.web.env.EnvironmentLoader.initEnvironment(EnvironmentLoader.java:141) INFO  - Shiro environment initialized in 80 ms.
```

## 注意,这里只是完成了一个独立配置(而且是允许一切的配置),还没与nutz进行深入集成.

### 后面会有章节独立说明与nutz集成的操作(需要建立相应的权限表和对应的pojo)