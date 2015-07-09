# 重建数据库

## 因为User表修改了, 也就是当前唯一的表, 所以,打开mysql控制台,执行下面的语句

```sql
drop table nutzbook.t_user;
```

### 其中nutzbook是数据库名,替换成你自己的数据库名就行.