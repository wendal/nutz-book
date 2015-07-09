# 新增UserService

## 新增服务类UserService,这次暂时不建接口了

```java
package net.wendal.nutzbook.service;

import java.util.Date;

import net.wendal.nutzbook.bean.User;

import org.apache.shiro.crypto.hash.Sha256Hash;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.lang.random.R;
import org.nutz.service.IdNameEntityService;

@IocBean(fields="dao")
public class UserService extends IdNameEntityService<User> {

	public User add(String name, String password) {
		User user = new User();
		user.setName(name.trim());
		user.setSalt(R.UU16());
		user.setPassword(new Sha256Hash(password, user.getSalt()).toHex());
		user.setCreateTime(new Date());
		user.setUpdateTime(new Date());
		return dao().insert(user);
	}
	
	public int fetch(String username, String password) {
		User user = fetch(username);
		if (user == null) {
			return -1;
		}
		String _pass = new Sha256Hash(password, user.getSalt()).toHex();
		if(_pass.equalsIgnoreCase(user.getPassword())) {
			return user.getId();
		}
		return -1;
	}
	
	public void updatePassword(int userId, String password) {
		User user = fetch(userId);
		if (user == null) {
			return;
		}
		user.setSalt(R.UU16());
		user.setPassword(new Sha256Hash(password, user.getSalt()).toHex());
		user.setUpdateTime(new Date());
		dao().update(user, "^(password|salt|updateTime)$");
	}
}

```

### 留意一下IocBean中的fields配置,含义是需要注入父类的dao属性
### 这里用到了sha256加盐算法,将对应shiro.ini中配置