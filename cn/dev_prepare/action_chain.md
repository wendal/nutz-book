# 配置动作链

### 动作链,很强大,但之前很少解释,导致很少人用到.

## 在conf文件夹中,新建一个文件夹mvc,新增一个配置文件叫nutzbook-mvc-chain.js, 内容如下

```js
var chain={
	"default" : {
		"ps" : [
		      "net.wendal.nutzbook.mvc.LogTimeProcessor",
		      "org.nutz.mvc.impl.processor.UpdateRequestAttributesProcessor",
		      "org.nutz.mvc.impl.processor.EncodingProcessor",
		      "org.nutz.mvc.impl.processor.ModuleProcessor",
		      "org.nutz.mvc.impl.processor.ActionFiltersProcessor",
		      "org.nutz.mvc.impl.processor.AdaptorProcessor",
		      "org.nutz.mvc.impl.processor.MethodInvokeProcessor",
		      "org.nutz.mvc.impl.processor.ViewProcessor"
		      ],
		"error" : 'org.nutz.mvc.impl.processor.FailProcessor'
	}
};
```

### 这个动作链配置文件,与nutz默认的配置文件,仅仅多了一行 ```net.wendal.nutzbook.mvc.LogTimeProcessor```

## 所以,新建一个类叫LogTimeProcessor, 包自然就是net.wendal.nutzbook.mvc咯, 继承org.nutz.mvc.impl.processor.AbstractProcessor

```java
package net.wendal.nutzbook.mvc;

import javax.servlet.http.HttpServletRequest;

import org.nutz.lang.Stopwatch;
import org.nutz.log.Log;
import org.nutz.log.Logs;
import org.nutz.mvc.ActionContext;
import org.nutz.mvc.impl.processor.AbstractProcessor;

public class LogTimeProcessor extends AbstractProcessor {
	
	private static final Log log = Logs.get();

	public LogTimeProcessor() {
	}

	@Override
	public void process(ActionContext ac) throws Throwable {
		Stopwatch sw = Stopwatch.begin();
		try {
			doNext(ac);
		} finally {
			sw.stop();
			if (log.isDebugEnabled()) {
				HttpServletRequest req = ac.getRequest();
				log.debugf("[%4s]URI=%s %sms", req.getMethod(), req.getRequestURI(), sw.getDuration());
			}
		}
	}

}

```

## 然后打开MainModule这个类,加入一个注解

```java
@ChainBy(args="mvc/nutzbook-mvc-chain.js")
```

## 启动tomcat并登陆登出,可以看到有类似的log输出

```
2015-04-09 19:46:59,140 net.wendal.nutzbook.mvc.LogTimeProcessor.process(LogTimeProcessor.java:27) DEBUG - [POST]URI=/nutzbook/user/login 30ms
```

### 这个类的主要目的是演示动作链的配置, 因为druid的监控页面有更详尽的统计数据了(以前可没有druid,呵呵)