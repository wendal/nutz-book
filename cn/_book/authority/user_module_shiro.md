# 修改UserModule的Shiro注解

打开UserModule类,修改注解的时候到了
--------------------------------

在之前的章节中,添加了@RequiresUser,现在全部删除,改成@RequiresPermissions(...), 例如add方法,改成

```java
@RequiresPermissions("user:add")
```

update方法改成

```java
@RequiresPermissions("user:update")
```

如此类推.