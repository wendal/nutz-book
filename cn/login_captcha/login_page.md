# 修改登陆页面

## 打开当前登陆表单所在的WebContent/index.jsp页面, 在下述代码

```html
密码 <input name="password" type="password" value="123456">
```

### 的后面加入

```html
		<script type="text/javascript">
			function next_captcha() {
				$("#captcha_img").attr("src", "${base}/captcha/next?_=" + new Date().getTime());
			}
		</script>
		验证码<input name="captcha" type="text" value="">
		<img id="captcha_img" onclick="next_captcha();return false;" src="${base}/captcha/next"></img>
```

## 将登陆的ajax回调方法也修改一下

```js
				success: function(data) {
					alert(data);
					if (data == true) {
						alert("登陆成功");
						location.reload();
					} else {
						alert("登陆失败,请检查账号密码")
					}
				}
```

### 改成

```js
				success: function(data) {
					if (data && data.ok) {
						alert("登陆成功");
						location.reload();
					} else {
						alert(data.msg);
					}
				}
```

### 目的就是实现显示验证码及接收后端新的反馈数据格式
