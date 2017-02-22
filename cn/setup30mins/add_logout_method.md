# 添加登出方法

## 在UserModule新增一个logout方法

```java
	@At
	@Ok(">>:/")
	public void logout(HttpSession session) {
		session.invalidate();
	}
```

验证? 你喜欢就访问一下logout的路径吧,我不管了... 只要不出Not Found就好了.

注意一下, 必须使用`>>:XXX` 即302重定向,不要使用`->:XXX`内部重定向, 因为后者在shiro环境下会报错.

* `>>` 和 `->` 分别是 `redirect` 和 `forward`的缩写.

想提前知道@Ok中内置的缩写? 看 org.nutz.mvc.view.DefaultViewMaker 的源码吧.

## 手册关联(选修)

* [URL 映射](http://nutzam.com/core/mvc/url_mapping.html)
* [适配器](http://nutzam.com/core/mvc/http_adaptor.html)
* [视图](http://nutzam.com/core/mvc/view.html)
