# 新增BaseModule类

## Module类的一些属性总是雷同的,所以,新建一个BaseModule类, package为net.wendal.nutzbook.module

```
package net.wendal.nutzbook.module;

import org.nutz.dao.Dao;
import org.nutz.ioc.loader.annotation.Inject;

public abstract class BaseModule {

	/** 注入同名的一个ioc对象 */
	@Inject protected Dao dao;

}
```

## 打开UserModule类,继承BaseModule,并删除dao属性(非常非常重要).

子类与超类的同名属性,会被屏蔽, 导致父类的同名属性没有赋值,调用时出现NPE
