# 新增BasePojo类

## 为了简化将来需要更多的Pojo(Bean),做个抽象的BasePojo,把共有的属性和方法统一一下.

## 类名为BasePojo, package自然是net.wendal.nutzbook.bean, Bean的内容如下

```
package net.wendal.nutzbook.bean;

import java.util.Date;

import org.nutz.dao.entity.annotation.Column;
import org.nutz.json.Json;
import org.nutz.json.JsonFormat;

public abstract class BasePojo {
	
	@Column("ct")
	protected Date createTime;
	@Column("ut")
	protected Date updateTime;
	
	public String toString() {
		return String.format("/*%s*/%s", super.toString(), Json.toJson(JsonFormat.compact()));
	}

	public Date getCreateTime() {
		return createTime;
	}

	public void setCreateTime(Date createTime) {
		this.createTime = createTime;
	}

	public Date getUpdateTime() {
		return updateTime;
	}

	public void setUpdateTime(Date updateTime) {
		this.updateTime = updateTime;
	}
}

```

### 可以看到,这个类带了@Column注解的属性,所以继承这个类的子类的数据库属性均需要标注@Column了.
### 另外这个类也覆盖了toString方法,默认输出为对象的Json字符串格式

## 修改User类, 使其继承BasePojo,并删除createTime和updateTime

```
package net.wendal.nutzbook.bean;

import org.nutz.dao.entity.annotation.Column;
import org.nutz.dao.entity.annotation.Id;
import org.nutz.dao.entity.annotation.Name;
import org.nutz.dao.entity.annotation.Table;

@Table("t_user")
public class User extends BasePojo {

	@Id
	private int id;
	@Name
	@Column
	private String name;
	@Column("passwd")
	private String password;
	@Column
	private String salt;
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
	public String getSalt() {
		return salt;
	}
	public void setSalt(String salt) {
		this.salt = salt;
	}
	
}
```