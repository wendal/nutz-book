# 添加管理页面

需要新增2个页面

第一个是WebContent/page/simple_role.jsp, 这是authority.jsp页面的外框
----------------------------------------

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>无框架的权限管理界面</title>
    <script src="${base}/rs/js/jquery.js"></script>
</head>
<body>
<jsp:include page="authority.jsp"></jsp:include>
<script type="text/javascript">
	var home_base = '${base}';
	$(function() {
		myInit();
	});
</script>
</body>
</html>
```

第二个当然是authority.jsp了, 有几百行,只能节选了
---------------------------------------------

```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<div class="row">
	<!-- 下面的ul是3个Table -->
	<ul class="md-tab-group">
		<li>
			<div class="ripple-button" id="_user_role" onclick="showTab('user_role')">用户权限一览</div>
		</li>
		<li>
			<div class="ripple-button" id="_roles" onclick="showTab('roles')">角色一览</div>
		</li>
		<li>
			<div class="ripple-button" id="_permissions" onclick="showTab('permissions')">权限一览</div>
		</li>
		<div class="tab-bottom"></div>
	</ul>

....................
....................
....................

<script type="text/javascript">
	_r = {};
	/*页面片段的初始化方法*/
	function myInit(args) {
		// 载入用户列表
		loadUsers();
		// 载入角色列表
		loadRoles();
		// 载入权限列表
		loadPermissions();
		// 默认显示用户列表的Tab
		$("#_user_role").click();
	};

....................
....................
....................

	/*新增一个权限*/
	function permission_add() {
		var permission_name = prompt("请输入新角色的名词,仅限英文字母/冒号/米号,长度3到30个字符");
		var re = /[a-zA-Z\:\*]{3,10}/;  
		if (permission_name && re.exec(permission_name)) {
			$.ajax({
				url : home_base + "/admin/authority/permission/add",
				type : "POST",
				data : JSON.stringify({name:permission_name}),
				success : function () {
					loadPermissions();
				}
			});
		}
	};
	
</script>
```

页面并没有多少美化,纯html, 点击XXX一览就切换不同的div