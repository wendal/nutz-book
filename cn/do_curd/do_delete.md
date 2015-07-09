# delete方法--删除指定用户

最直接的方法,通过id删除用户

```java
	@At
	public Object delete(@Param("id")int id, @Attr("me")int me) {
		if (me == id) {
			return new NutMap().setv("ok", false).setv("msg", "不能删除当前用户!!");
		}
		dao.delete(User.class, id); // 再严谨一些的话,需要判断是否为>0
		return new NutMap().setv("ok", true);
	}
```

留意一下,其中的@Attr是取Session/Request中的me属性.
