# 添加登出方法

## 在UserModule新增一个logout方法

```
	@At
	@Ok(">>:/")
	public void logout(HttpSession session) {
		session.invalidate();
	}
```

验证? 你喜欢就访问一下logout的路径吧,我不管了... 只要不出Not Found就好了