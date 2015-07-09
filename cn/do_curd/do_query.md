# query方法--根据条件查询用户

## 根据名字查就可以了,也没其他可以查询的信息了吧,当然加上分页咯

```java
	@At
	public Object query(@Param("name")String name, @Param("..")Pager pager) {
		Cnd cnd = Strings.isBlank(name)? null : Cnd.where("name", "like", "%"+name+"%");
		QueryResult qr = new QueryResult();
		qr.setList(dao.query(User.class, cnd, pager));
		pager.setRecordCount(dao.count(User.class, cnd));
		qr.setPager(pager);
		return qr; //默认分页是第1页,每页20条
	}
```

## 测试

直接查询

```
http://127.0.0.1:8080/nutzbook/user/query
```

带条件查询

```
http://127.0.0.1:8080/nutzbook/user/query?name=ad
```

带分页查询

```
http://127.0.0.1:8080/nutzbook/user/query?pageNumber=1&pageSize=2
```