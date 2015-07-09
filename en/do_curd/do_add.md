# add方法-增加用户

## 假设客户端通过表单把新建用户的属性都发送过来了, 那么在UserModule中就建一个add方法如下

```java
	@At
	public Object add(@Param("..")User user) {
		NutMap re = new NutMap();
		String msg = checkUser(user, true);
		if (msg != null){
			return re.setv("ok", false).setv("msg", msg);
		}
		user.setCreateTime(new Date());
		user.setUpdateTime(new Date());
		user = dao.insert(user);
		return re.setv("ok", true).setv("data", user);
	}
```

## 测试

访问如下URL, 会返回一个json字符串

```
http://127.0.0.1:8080/nutzbook/user/add?name=wendal&password=123456
```