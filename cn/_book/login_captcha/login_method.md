# 修改登陆方法

## 打开UserModule, 将login方法修改为

```java
	@At
	@Filters // 覆盖UserModule类的@Filter设置,因为登陆可不能要求是个已经登陆的Session
	public Object login(@Param("username")String name, 
			@Param("password")String password, 
			@Param("captcha")String captcha,
			@Attr(scope=Scope.SESSION, value="nutz_captcha")String _captcha,
			HttpSession session) {
		NutMap re = new NutMap();
		if (!Toolkit.checkCaptcha(_captcha, captcha)) {
			return re.setv("ok", false).setv("msg", "验证码错误");
		}
		User user = dao.fetch(User.class, Cnd.where("name", "=", name).and("password", "=", password));
		if (user == null) {
			return re.setv("ok", false).setv("msg", "用户名或密码错误");
		} else {
			session.setAttribute("me", user.getId());
			return re.setv("ok", true);
		}
	}
```

### 注意一下其中检查验证码的Toolkit.checkCaptcha方法.