# 新增Role类

## 新增类 net.wendal.nutzbook.bean.Role ,请自行补齐getter/setter

```java
package net.wendal.nutzbook.bean;

import java.util.List;

import org.nutz.dao.entity.annotation.ColDefine;
import org.nutz.dao.entity.annotation.Column;
import org.nutz.dao.entity.annotation.Id;
import org.nutz.dao.entity.annotation.ManyMany;
import org.nutz.dao.entity.annotation.Name;
import org.nutz.dao.entity.annotation.Table;

@Table("t_role")
public class Role extends BasePojo {
	
	@Id
	protected long id;
	@Name
	protected String name;
	@Column("al")
	protected String alias;
	@Column("dt")
	@ColDefine(type = ColType.VARCHAR, width = 500)
	private String description;
	@ManyMany(from="role_id", relation="t_role_permission", target=Permission.class, to="permission_id")
	protected List<Permission> permissions;
}
```