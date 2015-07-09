# 其他小Log

## 经过前面几个小节,还剩下3行没提及的log

```
2015-03-30 10:49:49,667 org.nutz.mvc.impl.NutLoading.createViewMakers(NutLoading.java:344) DEBUG - @Views(DefaultViewMaker)
2015-03-30 10:49:49,675 org.nutz.mvc.impl.NutLoading.createChainMaker(NutLoading.java:245) DEBUG - @ChainBy(org.nutz.mvc.impl.NutActionChainMaker)
2015-03-30 10:49:49,728 org.nutz.mvc.impl.NutLoading.evalLocalization(NutLoading.java:309) DEBUG - @Localization not define
```

## 就三行了,吃了它

* 第一条, 是@Views配置,当前MainModule并没有配置,所以这是默认配置,将来用到自定义View的时候自然会配置上
* 第二条, ChainBy是动作链配置, 是Mvc中的核心配置,也是当前很少人用到的强大配置之一, 下一章就会用到
* 第三条, 是国际化相关, 在稍后的章节中会开始使用.