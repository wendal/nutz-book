# 添加验证邮件的返回方法

## 这就是验证邮件里面的链接需要访问的入口方法咯

```java
	@Filters // 不需要先登录,很明显...
	@At("/active/mail")
	@GET
	@Ok("raw") // 为了简单起见,这里直接显示验证结果就好了
	public String activeMailCallback(@Param("token")String token, HttpSession session) {
		if (Strings.isBlank(token)) {
			return "请不要直接访问这个链接!!!";
		}
		if (token.length() < 10) {
			return "非法token";
		}
		try {
			token = Toolkit._3DES_decode(emailKEY, Toolkit.hexstr2bytearray(token));
			if (token == null)
				return "非法token";
			String[] tmp = token.split(",", 3);
			if (tmp.length != 3 || tmp[0].length() == 0 || tmp[1].length() == 0 || tmp[2].length() == 0)
				return "非法token";
			long time = Long.parseLong(tmp[2]);
			if (System.currentTimeMillis() - time > 10*60*1000) {
				return "该验证链接已经超时";
			}
			int userId = Integer.parseInt(tmp[0]);
			Cnd cnd = Cnd.where("userId", "=", userId).and("email", "=", tmp[1]);
			int re = dao.update(UserProfile.class, Chain.make("emailChecked", true), cnd);
			if (re == 1) {
				return "验证成功";
			}
			return "验证失败!!请重新验证!!";
		} catch (Throwable e) {
			log.debug("检查token时出错", e);
			return "非法token";
		}
	}
```

* 限定为GET请求,这样邮件里面直接按就好了
* 需要通过3DES解码token数据
* 通过验证dao.update的更新条数来判断是否成功,这样就验证了userId和email是否匹配.