# 修改User类

## 通过Daos.migration实现表结构自动修改

在MainSetup.init方法内, Daos.createTableInPackage之后添加:

```java
Daos.migration(dao, User.class, true, false, false);
```
