# 真实项目的集成步骤

## 基本步骤

* 参考NutDaoRealm实现一个符合项目需要的Realm,及对应的权限模型
* 添加或修改shiro.ini, 关联realm, 如有必要, 关联CaptchaFormAuthenticationFilter
* 在动作链中加入NutShiroProcessor
* 在入口方法中应用Shiro的注解

## Shiro插件jar中的其他类

* 帮助类 NutShiro -- 封装一些ajax判断等等.
* aop配置相关的NutShiroAopConfigure -- 为*所有*带Shiro注解的方法启用aop拦截
* @Filters版本的ShiroActionFilter -- 不建议使用,对于单个入口方法效果与NutShiroProcessor类似


## 项目打包, 为了方便大家,这次会把整个项目,含所有源码供大家下载.

[项目打包下载](nutz_shiro_project.zip)

### 正如本书的其他压缩包一样,如果发现bug,请报个issue哦, 也正是如此,这个压缩包可能会不时更新.