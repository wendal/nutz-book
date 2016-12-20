# 添加登陆方法

## 在UserModule类加入一个方法

```java
	@At
	public Object login(@Param("username")String name, @Param("password")String password, HttpSession session) {
		User user = dao.fetch(User.class, Cnd.where("name", "=", name).and("password", "=", password));
		if (user == null) {
			return false;
		} else {
			session.setAttribute("me", user.getId());
			return true;
		}
	}
```

## 启动tomcat验证一下

访问URL

```
http://127.0.0.1:8080/nutzbook/user/login?username=admin&password=123456
```

正常结果自然就是true了, 如果是false,检查一下MainSetup里面的密码有无写错, 如果报错,就看看具体堆栈的提示吧

## 手册关联(选修)

* [URL 映射](http://nutzam.com/core/mvc/url_mapping.html)
* [适配器](http://nutzam.com/core/mvc/http_adaptor.html)
* [视图](http://nutzam.com/core/mvc/view.html)
* [Dao接口基本操作](http://nutzam.com/core/dao/basic_operations.html)