# 新增UserProfile类

## 新建一个类,名为UserProfile,package自然就是net.wendal.nutzbook.bean, 继承BasePojo类 这个类是User类的详细信息类,与User是一对一关系

```java
package net.wendal.nutzbook.bean;

import java.sql.Blob;

import org.nutz.dao.entity.annotation.Column;
import org.nutz.dao.entity.annotation.Id;
import org.nutz.dao.entity.annotation.Table;

@Table("t_user_profile")
public class UserProfile extends BasePojo {

	/**关联的用户id*/
	@Id(auto=false)
	@Column("uid")
	protected int userId;
	/**用户昵称*/
	@Column
	protected String nickname;
	/**用户邮箱*/
	@Column
	protected String email;
	/**邮箱是否已经验证过*/
	@Column("email_checked")
	protected boolean emailChecked;
	/**头像的byte数据*/
	@Column
	@JsonField(ignore=true)
	protected byte[] avatar;
	/**性别*/
	@Column
	protected String gender;
	/**自我介绍*/
	@Column("dt")
	protected String description;
	@Column("loc")
	protected String location;
}
```

### 然后就添加Getter/Setter了,这次就不再说了.