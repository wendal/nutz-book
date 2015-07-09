# 改造profile.jsp

## 打开WebContent/WEB-INF/jsp/user/profile.jsp, 在这段代码后面

```
邮箱验证状态:<c:out value="${obj.emailChecked}"></c:out><p />
```

加入

```jsp
				<c:if test="${!obj.emailChecked}">
					<script type="text/javascript">
						function send_email_check() {
							$.ajax({
								url : base + "/user/profile/active/mail",
								type : "POST",
								dataType : "json",
								success : function (data) {
									if (data.ok) {
										alert("发送成功");
									} else {
										alert(data.msg);
									}
								}
							});
						}
					</script>
					<button type="button" onclick="send_email_check();return false;">发送验证邮件</button>
				</c:if>
```

### 含义是,如果邮箱未验证,则显示一个按键(隐藏一段js代码),用于触发发送验证邮件.