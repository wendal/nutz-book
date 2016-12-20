# 修改User类

## 通过Daos.migration实现表结构自动修改

```java
Daos.migration(dao, User.class, true, false);
```
