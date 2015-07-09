# 新增Permission类

## 新增类 net.wendal.nutzbook.bean.Permission ,请自行补齐getter/setter

```java
package net.wendal.nutzbook.bean;

import org.nutz.dao.entity.annotation.ColDefine;
import org.nutz.dao.entity.annotation.Column;
import org.nutz.dao.entity.annotation.Id;
import org.nutz.dao.entity.annotation.Name;
import org.nutz.dao.entity.annotation.Table;

@Table("t_permission")
public class Permission extends BasePojo {

	@Id
	protected long id;
	@Name
	protected String name;
	@Column("al")
	protected String alias;
	@Column("dt")
	@ColDefine(type = ColType.VARCHAR, width = 500)
	private String description;
}
```