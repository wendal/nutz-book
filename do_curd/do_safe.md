# 加强安全性

当前的增删改查,无论登陆与否都可以操作,实在太不靠谱了,所以,还是加个检查吧.

## 判断用户登陆

UserModule添加一个注解

```java
@Filters(@By(type=CheckSession.class, args={"me", "/"}))
```

含义是,如果当前Session没有带me这个attr,就跳转到/页面,即首页.

同时,为login方法设置为空的过滤器,不然就没法登陆了


```java
@Filters()
```


## 另外, 密码和salt也不可以发送到浏览器去.

将UserModule的@Ok注解改成

```java
@Ok("json:{locked:'password|salt',ignoreNull:true}")
```