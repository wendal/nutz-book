# 添加发送验证邮件的方法

## 打开BaseModule类,先添加2个属性

```java
@Inject protected EmailService emailService;

protected byte[] emailKEY = R.sg(24).next().getBytes();
```

## 打开UserProfileModule类,添加一个方法,哈哈, 这个方法会使用到net.wendal.nutzbook.util.Toolkit类, 如果没有, 就到*为正式开发做准备*一章补上吧.

```java
	@At("/active/mail")
	@POST
	public Object activeMail(@Attr(scope=Scope.SESSION, value="me")int userId,
			HttpServletRequest req) {
		NutMap re = new NutMap();
		UserProfile profile = get(userId);
		if (Strings.isBlank(profile.getEmail())) {
			return re.setv("ok", false).setv("msg", "你还没有填邮箱啊!");
		}
		String token = String.format("%s,%s,%s", userId, profile.getEmail(), System.currentTimeMillis());
		token = Toolkit._3DES_encode(emailKEY, token.getBytes());
		String url = req.getRequestURL() + "?token=" + token;
		String html = "<div>如果无法点击,请拷贝一下链接到浏览器中打开<p/>验证链接 %s</div>";
		html = String.format(html, url, url);
		try {
			boolean ok = emailService.send(profile.getEmail(), "XXX 验证邮件 by Nutzbook", html);
			if (!ok) {
				return re.setv("ok", false).setv("msg", "发送失败");
			}
		} catch (Throwable e) {
			log.debug("发送邮件失败", e);
			return re.setv("ok", false).setv("msg", "发送失败");
		}
		return re.setv("ok", true);
	}
```

* 看清楚,这个方法只接受POST请求,虽然没参数
* 用到了EmailService发邮件哦
* 用到了Toolkit._3DES_encode加密token
* 注意, 因为emailKEY每次启动都是新的,所以重启Tomcat后,老的验证邮件就无效了哦. 真正用到时候,一般会存到一个文件或者数据库里面去.