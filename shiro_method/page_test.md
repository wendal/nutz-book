# 页面测试

## 这次的页面测试就没啥难度了吧, 先强制登出

```
http://192.168.72.102:8080/nutzbook/user/logout
```

### 因为UserModule里面的logout方法已经删除,如果出现404,也只是shiro配置的问题了

## 一如既往,登陆, 成功后跳转到用户详情页

```
http://192.168.72.102:8080/nutzbook/user/login
```

## 访问用户列表页, 各种建用户改密码测试

```
http://192.168.72.102:8080/nutzbook/user/login
```