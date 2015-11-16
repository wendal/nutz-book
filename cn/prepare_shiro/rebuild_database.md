# 重建数据库

## 因为User表修改了, 所以,打开mysql控制台,执行下面的语句

```sql
drop table nutzbook.t_user;
```

如果使用了1.b.53或以上的版本,可以在MainSetup中自动修改

```
Daos.migration(dao, User.class, true, false);
```

### 其中nutzbook是数据库名,替换成你自己的数据库名就行.