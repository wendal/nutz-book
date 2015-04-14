# 头像读取方法


## 在UserProfileModule中再添加一个读取用户头像的方法

```java
	@Ok("raw:jpg")
	@At("/avatar")
	@GET
	public Object readAvatar(@Attr(scope=Scope.SESSION, value="me")int userId, HttpServletRequest req) throws SQLException {
		UserProfile profile = Daos.ext(dao, FieldFilter.create(UserProfile.class, "^avatar$")).fetch(UserProfile.class, userId);
		if (profile == null || profile.getAvatar() == null) {
			return new File(req.getServletContext().getRealPath("/rs/user_avatar/none.jpg"));
		}
		return profile.getAvatar().getBinaryStream();
	}
```

### 这里用到了Daos.ext方法,可以简单避免匿名内部类的使用, 因为只需要读取avatar字段.
### 取HttpServletRequest就是这么简单,直接声明一个参数就可以了. 同理resp也是.