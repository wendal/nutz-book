# 集成jetbrick-template-2x

## 基本信息

* 官网 http://subchen.github.io/jetbrick-template/
* 下载 http://subchen.github.io/jetbrick-template/2x/download.html
* 该模板的默认文件后缀是jetx,所以默认视图类型也就是jetx

通过maven下载集成jar

```
<dependency>
    <groupId>com.github.subchen</groupId>
    <artifactId>jetbrick-template-nutz</artifactId>
    <version>2.0.10</version>
</dependency>
```

## 开始集成, 先在conf目录下创建配置文件jetbrick-template.properties

```
jetx.template.loaders = $loader

$loader = jetbrick.template.loader.ServletResourceLoader
$loader.root = /WEB-INF/templates/jetx
$loader.reloadable = true
```

## 打开MainModule类, 添加一个注解,即可关联jetbrick-template. 

```
@Views({JetTemplateViewMaker.class})
```

## 然后我们新建一个模板 /WebContent/WEB-INF/templates/jetx/hello.jetx, 内容如下

```
<table>
  <tr>
    <td>序号</td>
    <td>姓名</td>
    <td>邮箱</td>
  </tr>
  #for (user : obj.list)
  <tr>
    <td>${for.index}</td>
    <td>${user.nickname}</td>
    <td>${user.email}</td>
  </tr>
  #end
</table>
```

## 然后新建一个模块叫JetTemplateModule, 用于测试

```java
package net.wendal.nutzbook.module;

import net.wendal.nutzbook.bean.UserProfile;

import org.nutz.dao.QueryResult;
import org.nutz.dao.pager.Pager;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.mvc.annotation.At;
import org.nutz.mvc.annotation.Ok;

@IocBean
@At("/jetx")
public class JetTemplateModule extends BaseModule {

	@At
	@Ok("jetx:hello.jetx")
	public Object hello() {
		QueryResult qr = new QueryResult();
		Pager pager = dao.createPager(1, 20);
		pager.setRecordCount(dao.count(UserProfile.class));
		qr.setPager(pager);
		qr.setList(dao.query(UserProfile.class, null, pager));
		return qr;
	}
}

```

启动项目,访问 http://127.0.0.1:8080/nutzbook/jetx/hello 即可看看效果
