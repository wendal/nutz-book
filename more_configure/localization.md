# 配置Localization

## 本地化,国际化. 在conf目录中,新建一个文件夹叫msg, 在里面再建一个文件文件夹zh-CN, 里面放一个空文件叫user.properties

![添加空的本地化字符串](images/localization_1.png)

## 打开MainModule,加入如下注解

```java
@Localization(value="msg/", defaultLocalizationKey="zh-CN")
```

## 启动正常的log如下

```
2015-04-10 12:11:14,780 org.nutz.mvc.impl.NutLoading.evalLocalization(NutLoading.java:281) DEBUG - Localization: org.nutz.mvc.impl.NutMessageLoader('msg/')  dft<zh-CN>
2015-04-10 12:11:14,783 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 1 resource by src( msg/ ) , regex( ^.+[.]properties$ )
2015-04-10 12:11:14,783 org.nutz.mvc.impl.NutMessageLoader.load(NutMessageLoader.java:29) DEBUG - Load Messages in 1 resource : [[NutResource[zh-CN/user.properties]]]
2015-04-10 12:11:14,785 org.nutz.mvc.impl.NutMessageLoader.load(NutMessageLoader.java:102) DEBUG - Message Loaded, size = 2
```