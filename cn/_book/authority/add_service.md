# 新增AuthorityService及其实现类

新增net.wendal.nutzbook.service.AuthorityService类
-----------------------------------------------------

```java
package net.wendal.nutzbook.service;

import net.wendal.nutzbook.bean.Role;
import net.wendal.nutzbook.bean.User;

public interface AuthorityService {

	/**
	 * 扫描RequiresPermissions和RequiresRoles注解
	 * @param pkg 需要扫描的package
	 */
	void initFormPackage(String pkg);
	
	/**
	 * 检查最基础的权限,确保admin用户-admin角色-(用户增删改查-权限增删改查)这一基础权限设置
	 * @param admin
	 */
	void checkBasicRoles(User admin);
	
	/**
	 * 添加一个权限
	 */
	public void addPermission(String permission);
	
	/**
	 * 添加一个角色
	 */
	public Role addRole(String role);
}
```

及其实现类AuthorityServiceImpl(节选)
-----------------------------------------

```java
	public void checkBasicRoles(User admin) {
		// 检查一下admin的权限
		Role adminRole = dao.fetch(Role.class, "admin");
		if (adminRole == null) {
			adminRole = addRole("admin");
		}
		// admin账号必须存在与admin组
		if (0 == dao.count("t_user_role", Cnd.where("u_id", "=", admin.getId()).and("role_id", "=", adminRole.getId()))) {
			dao.insert("t_user_role", Chain.make("u_id", admin.getId()).add("role_id", adminRole.getId()));
		}
		// admin组必须有authority:* 也就是权限管理相关的权限
		List<Record> res = dao.query("t_role_permission", Cnd.where("role_id", "=", adminRole.getId()));
		OUT: for (Permission permission : dao.query(Permission.class, Cnd.where("name", "like", "authority:%").or("name", "like", "user:%"), null)) {
			for (Record re : res) {
				if (re.getInt("permission_id") == permission.getId())
					continue OUT;
			}
			dao.insert("t_role_permission", Chain.make("role_id", adminRole.getId()).add("permission_id", permission.getId()));
		};
	}
```