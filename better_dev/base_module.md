# BaseModule类

为了后续开发的遍历,新增一个net.wendal.nutzbook.module.BaseModule,内容如下

```java
package net.wendal.nutzbook.module;

import java.util.List;

import net.wendal.nutzbook.service.EmailService;

import org.nutz.dao.Condition;
import org.nutz.dao.Dao;
import org.nutz.dao.QueryResult;
import org.nutz.dao.pager.Pager;
import org.nutz.ioc.loader.annotation.Inject;
import org.nutz.lang.util.NutMap;

public abstract class BaseModule {
	
	/** 注入与属性同名的一个ioc对象 */
	@Inject protected Dao dao;

	@Inject protected EmailService emailService;
	
	protected QueryResult query(Class<?> klass, Condition cnd, Pager pager, String regex) {
		if (pager != null && pager.getPageNumber() < 1) {
			pager.setPageNumber(1);
		}
		List<?> roles = dao.query(klass, cnd, pager);
		dao.fetchLinks(roles, null);
		pager.setRecordCount(dao.count(klass, cnd));
		return new QueryResult(roles, pager);
	}
	
	protected NutMap ajaxOk(Object data) {
		return new NutMap().setv("ok", true).setv("data", data);
	}
	
	protected NutMap ajaxFail(String msg) {
		return new NutMap().setv("ok", true).setv("msg", msg);
	}
}
```

这个类会随着项目的开发不断添加内容,所以在nutz-book-project中的这个类会复杂一些.

后续开发的Module类均继承BaseModule,省去一些重复的代码