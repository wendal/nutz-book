# 配置log4j

## 将log4j的jar包放入WebContent/WEB-INF/lib下面

![放置log4j的jar包](images/configure_log4j_1.png)

## 在conf目录中,新建一个文件,名为 log4j.properties 内容是

```
log4j.rootLogger=debug,Console

log4j.appender.Console=org.apache.log4j.ConsoleAppender
log4j.appender.Console.layout=org.apache.log4j.PatternLayout
log4j.appender.Console.layout.ConversionPattern=%d %l %-5p - %m%n

```

含义输出到控制台,以规定的格式