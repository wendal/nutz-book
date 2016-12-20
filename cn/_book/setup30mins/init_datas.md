## 初始化数据

## 打开MainSetup类,在Daos语句后面插入新建根用户的代码

```java
		// 初始化默认根用户
		if (dao.count(User.class) == 0) {
			User user = new User();
			user.setName("admin");
			user.setPassword("123456");
			user.setCreateTime(new Date());
			user.setUpdateTime(new Date());
			dao.insert(user);
		}
```

## 完成后的整个MainSetup类

```java
package net.wendal.nutzbook;

import java.util.Date;

import net.wendal.nutzbook.bean.User;

import org.nutz.dao.Dao;
import org.nutz.dao.util.Daos;
import org.nutz.ioc.Ioc;
import org.nutz.mvc.NutConfig;
import org.nutz.mvc.Setup;

public class MainSetup implements Setup {

  // 注意是init方法,不是depose方法
	public void init(NutConfig conf) {
		Ioc ioc = conf.getIoc();
		Dao dao = ioc.get(Dao.class);
		// 如果提示没有createTablesInPackage方法,请确认用了最新版的nutz,且老版本的nutz已经删除干净
		Daos.createTablesInPackage(dao, "net.wendal.nutzbook", false);

		// 初始化默认根用户
		if (dao.count(User.class) == 0) {
			User user = new User();
			user.setName("admin");
			user.setPassword("123456");
			user.setCreateTime(new Date());
			user.setUpdateTime(new Date());
			dao.insert(user);
		}
	}

	public void destroy(NutConfig conf) {
	}

}

```

## 启动Tomcat验证代码

在Servers选项页,右键Tomcat,点击Start, 或者 右键项目--Run as--Run on Server

如果一切顺利,项目很快就启动完成, 截图如下:

![](images/init_data_1.png)

## 观察tomcat输出的log

### Ioc初始化的日志,如果出错,请检查dao.js及IocBy的配置

```
2015-3-20 13:52:52.756 DEBUG [localhost-startStop-1] @IocBy(type=org.nutz.mvc.ioc.provider.ComboIocProvider, args=["*js", "ioc/", "*anno", "net.wendal.nutzbook", "*tx"])
2015-3-20 13:52:52.770 DEBUG [localhost-startStop-1] Found 1 resource by src( ioc/ ) , regex( ^(.+[.])(js|json)$ )
2015-3-20 13:52:52.770 DEBUG [localhost-startStop-1] loading ioc js config from [dao.js]
2015-3-20 13:52:52.776 DEBUG [localhost-startStop-1] Loaded 2 bean define from path=[ioc/] --> [dataSource, dao]
2015-3-20 13:52:52.778 DEBUG [localhost-startStop-1] Found 3 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-3-20 13:52:52.786 WARN [localhost-startStop-1] NONE Annotation-Class found!! Check your configure or report a bug!! packages=[net.wendal.nutzbook]
2015-3-20 13:52:52.787 DEBUG [localhost-startStop-1] Loaded 5 bean define from reader --
[txREPEATABLE_READ, txSERIALIZABLE, txNONE, txREAD_UNCOMMITTED, txREAD_COMMITTED]
```


### 建立数据库连接并创建表的log.

```
2015-3-20 13:52:52.955 DEBUG [localhost-startStop-1] Jdbcs init complete
2015-3-20 13:52:52.955 INFO [localhost-startStop-1] Get Connection from DataSource for JdbcExpert
2015-3-20 13:52:53.201 DEBUG [localhost-startStop-1] JDBC Driver --> mysql-connector-java-5.1.34 ( Revision: jess.balint@oracle.com-20141014163213-wqbwpf1ok2kvo1om )
2015-3-20 13:52:53.202 DEBUG [localhost-startStop-1] JDBC Name   --> MySQL Connector Java
2015-3-20 13:52:53.202 DEBUG [localhost-startStop-1] Database info --> MYSQL:[MySQL - 5.5.5-10.1.2-MariaDB]
2015-3-20 13:52:53.209 DEBUG [localhost-startStop-1] Found 3 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-3-20 13:52:53.252 DEBUG [localhost-startStop-1] Table 't_user' doesn't exist!
2015-3-20 13:52:53.268 DEBUG [localhost-startStop-1] Table 't_user' doesn't exist!
2015-3-20 13:52:53.271 DEBUG [localhost-startStop-1] CREATE TABLE t_user(
id INT(32) AUTO_INCREMENT,
name VARCHAR(50) UNIQUE NOT NULL,
passwd VARCHAR(50),
salt VARCHAR(50),
ct DATETIME,
ut DATETIME,
PRIMARY KEY (id)
) ENGINE=InnoDB CHARSET=utf8
2015-3-20 13:52:53.320 DEBUG [localhost-startStop-1] SELECT COUNT(*) FROM t_user
2015-3-20 13:52:53.329 DEBUG [localhost-startStop-1] INSERT INTO t_user(name,passwd,salt,ct,ut) VALUES(?,?,?,?,?)
    |     1 |      2 |    3 |                   4 |                   5 |
    |-------|--------|------|---------------------|---------------------|
    | admin | 123456 | NULL | 2015-03-20 13:52:53 | 2015-03-20 13:52:53 |
  For example:> "INSERT INTO t_user(name,passwd,salt,ct,ut) VALUES('admin','123456',NULL,'2015-03-20 13:52:53','2015-03-20 13:52:53') "
2015-3-20 13:52:53.346 DEBUG [localhost-startStop-1] SELECT @@IDENTITY
2015-3-20 13:52:53.347 INFO [localhost-startStop-1] Nutz.Mvc[nutz] is up in 658ms

```

如果出错:

* 检查dao.js里面的用户名,密码,数据库名称是否正确
* 确认数据库已经启动
* 检查IocBy是否写错
* 检查SetupBy的代码是否抄错, 通常是init和destroy写反了

## 完成后,关闭Tomcat

方法就不再重复了...

## 手册关联(选修)

无
