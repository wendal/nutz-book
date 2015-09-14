# 配置Mail相关的ioc文件

## 打开dao.js, 把conf的定义改一下, 使其能扫描到custom下面所有的配置文件

```json
		conf : {
			type : "org.nutz.ioc.impl.PropertiesProxy",
			fields : {
				paths : ["custom/"]
			}
		},
```

## 新增一个文件,路径为 conf/custom/mail.properties 内容如下

```ini
mail.HostName=smtp.exmail.qq.com
mail.SmtpPort=465
mail.UserName=nutzbook@wendal.net
mail.Password=book@2015
mail.SSLOnConnect=true
mail.From=nutzbook@wendal.net
mail.charset=UTF-8
```

### 注意,上述账号只是测试用的,密码随时更改,请使用您自己的QQ邮箱信息及服务器地址

## 再新增一个文件, 路径为 conf/ioc/mail.js 内容如下

```js
var ioc={
	emailAuthenticator : {
		type : "org.apache.commons.mail.DefaultAuthenticator",
		args : [{java:"$conf.get('mail.UserName')"}, {java:"$conf.get('mail.Password')"}]
	},
	htmlEmail : {
		type : "org.apache.commons.mail.ImageHtmlEmail",
		singleton : false,
		fields : {
			hostName : {java:"$conf.get('mail.HostName')"},
			smtpPort : {java:"$conf.get('mail.SmtpPort')"},
			authenticator : {refer:"emailAuthenticator"},
			SSLOnConnect : {java:"$conf.get('mail.SSLOnConnect')"},
			from : {java:"$conf.get('mail.From')"},
			charset : {java:"$conf.get('mail.charset', 'UTF-8')"}
		}
	}	
};
```

### 含义是, 声明一个非单例的HtmlEmail定义,配置信息均通过conf对象获取.

## 在MainSetup类的init方法末尾,加入下列测试代码

```java
		// 测试发送邮件
		try {
			HtmlEmail email = ioc.get(HtmlEmail.class);
			email.setSubject("测试NutzBook");
			email.setMsg("This is a test mail ... :-)" + System.currentTimeMillis());
			email.addTo("vt400@qq.com");//请务必改成您自己的邮箱啊!!!
			email.buildMimeMessage();
			email.sendMimeMessage();
		} catch (Exception e) {
			e.printStackTrace();
		}
```

## 启动Tomcat,观察日志输出, 如无异常, 您填写的邮箱将会收到一封邮件, 然后务必把上诉测试代码删除!!

* 抛出端口错误之类的错误: 请使用QQ邮箱等国内地址, 并确保dao.js修改正确
* 登陆失败,检查一下mail.properties的账号密码,服务器地址等等
* 发送失败, 别尝试发送给gmail之类的,发自己的QQ邮箱最靠谱

## 删除测试代码!!! 务必删除,否则每次启动都发送一封邮件了, 然后容易被封账号.