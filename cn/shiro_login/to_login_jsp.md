# 添加跳转方法

## 打开UserModule类,添加一个方法

```java
	@GET
	@At("/login")
	@Filters
	@Ok("jsp:jsp.user.login") // 降内部重定向到登录jsp
	public void loginPage() {}
```

### 含义是, 访问这个路径的GET请求,将会转发到 /WEB-INF/jsp/user/login.jsp