# 新的User类

## 新的User类,加上了locked属性及权限相关属性

```java
package net.wendal.nutzbook.bean;

import java.util.List;

import org.nutz.dao.entity.annotation.ColDefine;
import org.nutz.dao.entity.annotation.Column;
import org.nutz.dao.entity.annotation.Id;
import org.nutz.dao.entity.annotation.ManyMany;
import org.nutz.dao.entity.annotation.Name;
import org.nutz.dao.entity.annotation.One;
import org.nutz.dao.entity.annotation.Table;

@Table("t_user")
public class User extends BasePojo {

	@Id
	protected int id;
	@Name
	@Column
	protected String name;
	@Column("passwd")
	@ColDefine(width=128)
	protected String password;
	@Column
	protected String salt;
	@Column
	private boolean locked;
	@ManyMany(from="u_id", relation="t_user_role", target=Role.class, to="role_id")
	protected List<Role> roles;
	@ManyMany(from="u_id", relation="t_user_permission", target=Permission.class, to="permission_id")
	protected List<Permission> permissions;
	@One(target=UserProfile.class, field="id", key="userId")
	protected UserProfile profile;
}
```