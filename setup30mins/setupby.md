# 配置SetupBy

## 新建一个类叫MainSetup,package设置为net.wendal.nutzbook

![](images/setupby_1.png)

## MainSetup需要实现Setup接口,并在其中初始化数据库表

```
package net.wendal.nutzbook;

import org.nutz.dao.Dao;
import org.nutz.dao.util.Daos;
import org.nutz.ioc.Ioc;
import org.nutz.mvc.NutConfig;
import org.nutz.mvc.Setup;

public class MainSetup implements Setup {

	public void init(NutConfig conf) {
		Ioc ioc = conf.getIoc();
		Dao dao = ioc.get(Dao.class);
		Daos.createTablesInPackage(dao, "net.wendal.nutzbook", false);
	}
	
	public void destroy(NutConfig conf) {
	}

}

```

## 打开MainModule类, 配置@SetupBy, 引用刚刚创建的MainSetup

```
@SetupBy(value=MainSetup.class)
```

## 完成后的MainModule类

![](images/setupby_2.png)