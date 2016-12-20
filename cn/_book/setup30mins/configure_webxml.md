# 配置Web.xml文件

### 双击打开WebContent/WEB-INF/web.xml

在display-name节点和welcome-file-list节点之间,添加以下内容

```xml
  <filter>
  	<filter-name>nutz</filter-name>
  	<filter-class>org.nutz.mvc.NutFilter</filter-class>
  	<init-param>
  		<param-name>modules</param-name>
  		<param-value>net.wendal.nutzbook.MainModule</param-value>
  	</init-param>
  </filter>
  <filter-mapping>
  	<filter-name>nutz</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
```

## 完成后完整的web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
  <display-name>nutzbook</display-name>
  <filter>
  	<filter-name>nutz</filter-name>
  	<filter-class>org.nutz.mvc.NutFilter</filter-class>
  	<init-param>
  		<param-name>modules</param-name>
  		<param-value>net.wendal.nutzbook.MainModule</param-value>
  	</init-param>
  </filter>
  <filter-mapping>
  	<filter-name>nutz</filter-name>
  	<url-pattern>/*</url-pattern>
    <!-- ForwardView需要下面的配置 @Ok("->:/xxx/yyy/zzz") -->
	  <dispatcher>REQUEST</dispatcher>
	  <dispatcher>FORWARD</dispatcher>
	  <dispatcher>INCLUDE</dispatcher>
  </filter-mapping>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

## 手册关联(选修)

* [如何配置 web.xml](http://nutzam.com/core/mvc/web_xml.html)