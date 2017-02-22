# 配置IocBy

## 打开MainModule类, 添加IocBy配置,如下


```java
// 请注意星号!!不要拷贝少了
@IocBy(type=ComboIocProvider.class, args={"*js", "ioc/",
                       // 这个package下所有带@IocBean注解的类,都会登记上
										   "*anno", "net.wendal.nutzbook",
										   "*tx", // 事务拦截 aop
										   "*async"}) // 异步执行aop
```

记得导入相关的类哦, Ctrl+Shift+O

## 完成后的MainModule

```java
package net.wendal.nutzbook;

import org.nutz.mvc.annotation.IocBy;
import org.nutz.mvc.annotation.Modules;
import org.nutz.mvc.ioc.provider.ComboIocProvider;

@IocBy(type=ComboIocProvider.class, args={"*js", "ioc/",
										   "*anno", "net.wendal.nutzbook",
										   "*tx", // 事务拦截 aop
										   "*async"}) // 异步执行aop
@Modules(scanPackage=true)
public class MainModule {
}

```

## 简单解释一下

* ComboIocProvider的args参数, 星号开头的是类名或内置缩写,剩余的是各加载器的参数
* `*js` 是JsonIocLoader,负责加载js/json结尾的ioc配置文件
* `*anno` 是AnnotationIocLoader,负责处理注解式Ioc, 例如@IocBean
* `*tx` 是TransIocLoader,负责加载内置的事务拦截器定义, 1.b.52开始自带

## 手册关联(选修)

* [同Ioc容器一起工作](http://nutzam.com/core/mvc/with_ioc.html)
