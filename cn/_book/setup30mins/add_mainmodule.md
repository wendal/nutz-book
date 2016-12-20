# 添加MainModule

### 按Ctrl+N,选Class,点Next,输入package为net.wendal.nutzbook,类名为MainModule

![添加MainModule](images/add_mainmodule.png)

## 添加模块类自动扫描

添加一行代码

```java
	@Modules(scanPackage=true)
```
并按下Ctrl+Shift+O,自动导入.

![模块类自动扫描](images/add_mainmodule_modules.png)

## 手册关联(选修)

* [主模块-子模块-入口函数](http://nutzam.com/core/mvc/modules.html)