# 配置druid监控

druid 提供了一个web端的监控页面, 搭建起来不算麻烦, 建议添加.

## 打开web.xml, 在nutz的filter之前, 加入Web监控的配置

```xml
	<filter>
		<filter-name>DruidWebStatFilter</filter-name>
		<filter-class>com.alibaba.druid.support.http.WebStatFilter</filter-class>
		<init-param>
			<param-name>exclusions</param-name>
			<param-value>*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*,/rs/*</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>DruidWebStatFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
```

## 在welcome-file之前,再加入

```xml
	<servlet>
		<servlet-name>DruidStatView</servlet-name>
		<servlet-class>com.alibaba.druid.support.http.StatViewServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>DruidStatView</servlet-name>
		<url-pattern>/druid/*</url-pattern>
	</servlet-mapping>
```

### 本章结尾会提供当前项目的压缩包,如果不明白就下载压缩包看看吧

## 启动tomcat,先尝试登陆登出一次,然后访问如下地址观察效果

查看web统计信息

```
http://127.0.0.1:8080/nutzbook/druid/webapp.html
```

查询数据库操作的统计信息

```
http://127.0.0.1:8080/nutzbook/druid/sql.html
```

![Druid监控页面初探](images/druid_monitor.png)
