# 容器重要信息的Log

## 把相关的log给揪出来

```
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:55) INFO  - Nutz Version : 1.r.59
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:56) INFO  - Nutz.Mvc[nutz] is initializing ...
2015-03-30 10:49:49,525 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:60) DEBUG - Web Container Information:
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:61) DEBUG -  - Default Charset : UTF-8
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:62) DEBUG -  - Current . path  : D:\nutzbook\eclipse\.
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:63) DEBUG -  - Java Version    : 1.8.0_112
2015-03-30 10:49:49,526 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:64) DEBUG -  - File separator  : \
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:65) DEBUG -  - Timezone        : Asia/Shanghai
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:66) DEBUG -  - OS              : Windows 7 amd64
2015-03-30 10:49:49,527 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:67) DEBUG -  - ServerInfo      : Apache Tomcat/8.0.20
2015-03-30 10:49:49,528 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:68) DEBUG -  - Servlet API     : 3.1
2015-03-30 10:49:49,528 org.nutz.mvc.impl.NutLoading.load(NutLoading.java:70) DEBUG -  - ContextPath     : /nutzbook
2015-03-30 10:49:49,529 org.nutz.mvc.impl.NutLoading.createContext(NutLoading.java:217) DEBUG - >> app.root = D:/nutzbook/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/nutzbook

```

## 一一解剖

* 第一条, Nutz版本信息, 一般来说,默认回答问题都是按最新版来考虑
* 第二条, 注意中括号里面值,这个值就是web.xml中NutFilter的名字
* 第三条, 就是个抬头
* 第四条, 默认编码,非常非常非常非常重要,请按之前的准备章节的配置,这里必然是UTF-8,不然,请检查人品,不行就充值一下吧
* 第五条, 当前.路径,也就是当前工作目录, 通常配错log4j文件输出路径的时候,就可以到这里找了
* 第六条, Java的版本号, 有时候系统装了N个JDK,这里就能看出来到底用了啥
* 第七条, 文件路径分隔符,拼路径的时候有用
* 第八条, 操作系统的信息
* 第九条, Web容器的信息, ```Apache Tomcat/8.0.20``` 多明白的信息,哈哈
* 第十条, Servelt API的版本号,一般依赖于Web容器的版本
* 第十一条, ContentPath, 也就是在${base}所指代的值,如果是ROOT应用,这里就是空字符串
* 第十二条, 该web项目在tomcat中的真实路径,有时候说某某资源找不到,到这个目录下确认之

## 为啥显示这些信息?

日志的好处在于观察日志的变化就可以明白程序中的状态.

记得在反馈那小节提到的内容不? "完整的Nutz日志信息", 这些信息都有助于筛选,重现特定的问题.
