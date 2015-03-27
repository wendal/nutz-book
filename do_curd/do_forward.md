# 页面中转方法

因为我们打算把jsp放在WEB-INF下,然后WEB-INF下的文件是不能直接访问的,所以加个跳转的方法

```
	@At("/")
	@Ok("jsp:jsp.user.list") // 真实路径是 /WEB-INF/jsp/user/list.jsp
	public void index() {
	}
```

## 手册关联(选修)

* [视图](http://nutzam.com/core/mvc/view.html)