# 修改MainModule

## 打开MainModule, 添加一个注解

```
@SessionBy(ShiroSessionProvider.class)
```

含义是,使用Shiro的Session替换NutFilter作用域内的Session