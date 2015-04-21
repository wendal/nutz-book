# 新增CaptchaModule模块类

## 新增一个类 net.wendal.nutzbook.module.CaptchaModule

```java
package net.wendal.nutzbook.module;

import java.awt.image.BufferedImage;

import javax.servlet.http.HttpSession;

import net.wendal.nutzbook.util.Toolkit;

import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.mvc.annotation.At;
import org.nutz.mvc.annotation.Ok;
import org.nutz.mvc.annotation.Param;

import cn.apiclub.captcha.Captcha;
import cn.apiclub.captcha.backgrounds.GradiatedBackgroundProducer;
import cn.apiclub.captcha.gimpy.FishEyeGimpyRenderer;

@IocBean
@At("/captcha")
public class CaptchaModule {

	@At
	@Ok("raw:png")
	public BufferedImage next(HttpSession session, @Param("w") int w, @Param("h") int h) {
		if (w * h < 1) { //长或宽为0?重置为默认长宽.
			w = 200;
			h = 60;
		}
		Captcha captcha = new Captcha.Builder(w, h)
								.addText().addBackground(new GradiatedBackgroundProducer())
//								.addNoise(new StraightLineNoiseProducer()).addBorder()
								.gimp(new FishEyeGimpyRenderer())
								.build();
		String text = captcha.getAnswer();
		session.setAttribute(Toolkit.captcha_attr, text);
		return captcha.getImage();
	}
}
```

### 关键点

* raw代表RawView
* png是RawView中对image/png的缩写,是数据mime的描述
* 返回值是BufferedImage,且这是image/png, 所以会转为图片显示. 还支持jpg/webp等格式,详情参考RawView的源码吧.
* Captcha有N多的组合和配置,自行选择啦.