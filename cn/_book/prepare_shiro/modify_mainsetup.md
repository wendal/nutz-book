# 修改MainSetup

## 现在有了UserService,那么就不再需要笨拙地建User了, 创建根管理员的代码改成

```java
		// 初始化默认根用户
		if (dao.count(User.class) == 0) {
			UserService us = ioc.get(UserService.class);
			us.add("admin", "123456");
		}
```