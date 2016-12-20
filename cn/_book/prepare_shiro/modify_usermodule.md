# 修改UserModule

## 打开UserModule, 先加一个属性UserService

```java
	@Inject protected UserService userService;
```

## 因为密码加密了,所以登陆方法要改一下


请注意一下 SecurityUtils 那一行.

```java
	@At
	@Filters // 覆盖UserModule类的@Filter设置,因为登陆可不能要求是个已经登陆的Session
	@POST
	public Object login(@Param("username")String username, 
			@Param("password")String password, 
			@Param("captcha")String captcha,
			@Attr(scope=Scope.SESSION, value="nutz_captcha")String _captcha,
			HttpSession session) {
		NutMap re = new NutMap();
		if (!Toolkit.checkCaptcha(_captcha, captcha)) {
			return re.setv("ok", false).setv("msg", "验证码错误");
		}
		int userId = userService.fetch(username, password);
		if (userId < 0) {
			return re.setv("ok", false).setv("msg", "用户名或密码错误");
		} else {
			session.setAttribute("me", userId);
			// 完成nutdao_realm后启用.
			// SecurityUtils.getSubject().login(new SimpleShiroToken(userId));
			return re.setv("ok", true);
		}
	}
```


### 严重注意一下@Param("username") 待会要修改登陆页面的表单哦

## 同样的,修改一下add方法

```java
	@At
	public Object add(@Param("..")User user) { // 两个点号是按对象属性一一设置
		NutMap re = new NutMap();
		String msg = checkUser(user, true);
		if (msg != null){
			return re.setv("ok", false).setv("msg", msg);
		}
		user = userService.add(user.getName(), user.getPassword());
		return re.setv("ok", true).setv("data", user);
	}
```

## 还有update方法

```java
	@At
	public Object update(@Param("password")String password, @Attr("me")int me) {
		if (Strings.isBlank(password) || password.length() < 6)
			return new NutMap().setv("ok", false).setv("msg", "密码不符合要求");
		userService.updatePassword(me, password);
		return new NutMap().setv("ok", true);
	}
```