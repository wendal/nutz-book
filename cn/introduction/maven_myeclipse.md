# 关于Maven和MyEclipse的说明

## QQ群里反馈有这些问题及解决方法

* Maven下报配置文件未能找到 -- 提前添加log4j的配置文件到resources文件夹
* MyEclipse下修改UTF-8编码无效 -- 在配置里面修改workspace的编码,及tomcat的JVM启动参数(加入-Dfile.encoding=utf-8)

## Maven项目

在nutz-book-project的源码中, 有pom.xml