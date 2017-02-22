# 配置NutFilter需要忽略的路径

我们需要实现的功能是: /druid或/rs下的路径,就无条件跳过NutFilter

### 打开web.xml,配置exclusions

```xml
<filter>
	<filter-name>nutz</filter-name>
	<filter-class>org.nutz.mvc.NutFilter</filter-class>
	<init-param>
		<param-name>modules</param-name>
		<param-value>net.wendal.nutzbook.MainModule</param-value>
	</init-param>
	<init-param>
		<param-name>exclusions</param-name>
		<param-value>/rs/*,/druid/*</param-value>
	</init-param>
</filter>
```

## 启动tomcat, 应无异常.
