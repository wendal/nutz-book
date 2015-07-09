# 添加新Service

## 新建一个类EmailService, package为net.wendal.nutzbook.service ,内容如下

```java
package net.wendal.nutzbook.service;

public interface EmailService {

	boolean send(String to, String subject, String html);

}
```

## 再新建一个实现类 EmailServiceImpl

```java
package net.wendal.nutzbook.service;

import org.apache.commons.mail.HtmlEmail;
import org.nutz.ioc.Ioc;
import org.nutz.ioc.loader.annotation.Inject;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.log.Log;
import org.nutz.log.Logs;

@IocBean(name="emailService")
public class EmailServiceImpl implements EmailService {

	private static final Log log = Logs.get();
	
	@Inject("refer:$ioc")
	protected Ioc ioc;

	public boolean send(String to, String subject, String html) {
		try {
			HtmlEmail email = ioc.get(HtmlEmail.class);
			email.setSubject(subject);
			email.setHtmlMsg(html);
			email.addTo(to);
			email.send();
			return true;
		} catch (Throwable e) {
			log.info("send email fail", e);
			return false;
		}
	}
}

```

### 内容很简单,就是取出HtmlEmail然后发送出去.
