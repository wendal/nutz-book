# 新增AuthorityModule

新增net.wendal.nutzbook.module.AuthorityModule类(代码节选),整个类有300+行
--------------------------------------------------------

```java
@At("/admin/authority")
@IocBean
@Ok("void")//避免误写导致敏感信息泄露到服务器外
public class AuthorityModule extends BaseModule {
	/**
	 * 更新用户所属角色/特许权限
	 */
	@POST
	@AdaptBy(type=JsonAdaptor.class)
	@RequiresPermissions("authority:user:update")
	@At("/user/update")
	@Aop(TransAop.READ_COMMITTED)
	public void updateUser(@Param("user")User user,
						   @Param("roles")List<Long> roles, 
						   @Param("permissions")List<Long> permissions) {
		// 防御一下
		if (user == null)
			return;
		user = dao.fetch(User.class, user.getId());
		// 就在那么一瞬间,那个用户已经被其他用户删掉了呢
		if (user == null)
			return;
		if (roles != null) {
			List<Role> rs = new ArrayList<Role>(roles.size());
			for (long roleId : roles) {
				Role r = dao.fetch(Role.class, roleId);
				if (r != null) {
					rs.add(r);
				}
			}
			dao.fetchLinks(user, "roles");
			if (user.getRoles().size() > 0) {
				dao.clearLinks(user, "roles");
			}
			user.setRoles(rs);
			dao.insertRelation(user, "roles");
		}
		if (permissions != null) {
			List<Permission> ps = new ArrayList<Permission>();
			for (long permissionId : permissions) {
				Permission p = dao.fetch(Permission.class, permissionId);
				if (p != null)
					ps.add(p);
			}
			dao.fetchLinks(user, "permissions");
			if (user.getPermissions().size() > 0) {
				dao.clearLinks(user, "permissions");
			}
			user.setPermissions(ps);
			dao.insertRelation(user, "permissions");
		}
	}
}
```

关注点
-------------------

* 观察@At入口方法总是带有@RequiresPermissions(...)这种Shiro注解
* @Aop(TransAop.READ_COMMITTED) 事务安全
* dao.xxxxxRelation 多对多映射管理
* @AdaptBy(type=JsonAdaptor.class) 以json接受数据,解决表单传值容易出现串值的问题