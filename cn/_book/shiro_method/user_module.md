# 修改UserModule类

## 打开UserModule,找到SecurityUtils那一行,去掉注释

```java
SecurityUtils.getSubject().login(new SimpleShiroToken(userId));
```

这句login的SimpleShiroToken,将传给SimpleAuthorizingRealm的doGetAuthenticationInfo方法,完成shiro层的登录操作

## 删除所有@Filters的行

## 为add/update/delete/query/index, 加入shiro注解

```java
	@RequiresUser
```

### 当前还没有使用```@RequiresPermissions```,并非不支持,而只是因为当前权限表里面啥都没有,如果加上需要特定权限的注解,就啥都没法访问了,呵呵

### 当前的配置已经可以在入口方法使用shiro的5种注解.

## 同理,UserProfileModule也做相应修改,但请测试完成后再做,免得节外生枝.

* 细节自己搞定吧, 触类旁通哦. 提醒一句, activeMailCallback不需要加哦