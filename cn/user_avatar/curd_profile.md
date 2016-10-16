# UserProfile增删改查方法

## Pojo建好,那我们弄个模块吧, 新建一个类UserProfileModule, 包为net.wendal.nutzbook.module

```java
package net.wendal.nutzbook.module;

import java.util.Date;

import net.wendal.nutzbook.bean.UserProfile;

import org.nutz.dao.FieldFilter;
import org.nutz.dao.util.Daos;
import org.nutz.ioc.loader.annotation.IocBean;
import org.nutz.mvc.Scope;
import org.nutz.mvc.adaptor.JsonAdaptor;
import org.nutz.mvc.annotation.AdaptBy;
import org.nutz.mvc.annotation.At;
import org.nutz.mvc.annotation.Attr;
import org.nutz.mvc.annotation.By;
import org.nutz.mvc.annotation.Filters;
import org.nutz.mvc.annotation.Ok;
import org.nutz.mvc.annotation.Param;
import org.nutz.mvc.filter.CheckSession;

@IocBean
@At("/user/profile")
@Filters(@By(type=CheckSession.class, args={"me", "/"})) // 检查当前Session是否带me这个属性
public class UserProfileModule extends BaseModule {

	@At
	public UserProfile get(@Attr(scope=Scope.SESSION, value="me")int userId) {
		UserProfile profile = Daos.ext(dao, FieldFilter.locked(UserProfile.class, "avatar")).fetch(UserProfile.class, userId);
		if (profile == null) {
			profile = new UserProfile();
			profile.setUserId(userId);
			profile.setCreateTime(new Date());
			profile.setUpdateTime(new Date());
			dao.insert(profile);
		}
		return profile;
	}

	@At
	@AdaptBy(type=JsonAdaptor.class)
	@Ok("void")
	public void update(@Param("..")UserProfile profile, @Attr(scope=Scope.SESSION, value="me")int userId) {
		if (profile == null)
			return;
		profile.setUserId(userId);//修正userId,防止恶意修改其他用户的信息
		profile.setUpdateTime(new Date());
		profile.setAvatar(null); // 不准通过这个方法更新
		UserProfile old = get(userId);
		// 检查email相关的更新
		if (old.getEmail() == null) {
			// 老的邮箱为null,所以新的肯定是未check的状态
			profile.setEmailChecked(false);
		} else {
			if (profile.getEmail() == null) {
				profile.setEmail(old.getEmail());
				profile.setEmailChecked(old.isEmailChecked());
			} else if (!profile.getEmail().equals(old.getEmail())) {
				// 设置新邮箱,果断设置为未检查状态
				profile.setEmailChecked(false);
			} else {
				profile.setEmailChecked(old.isEmailChecked());
			}
		}
		Daos.ext(dao, FieldFilter.create(UserProfile.class, null, "avatar", true)).update(profile);
	}
}
```

### 可以看到,事实上只有取和更新的操作, 删除和新建(主动新建)是不实现的. 同时,这里用到了JsonAdaptor,所以前端发送过来的内容需要是个json了

## 删除User的时候也删除UserProfile. 打开UserModule类,修改delete方法

```java
	@At
	@Aop(TransAop.READ_COMMITTED)
	public Object delete(@Param("id")int id, @Attr("me")int me) {
		if (me == id) {
			return new NutMap().setv("ok", false).setv("msg", "不能删除当前用户!!");
		}
		dao.delete(User.class, id); // 再严谨一些的话,需要判断是否为>0
		dao.clear(UserProfile.class, Cnd.where("userId", "=", me));
		return new NutMap().setv("ok", true);
	}
```

### 留意一下,因为有多个数据库操作,这里加上了事务,这不是必须的.

这里的

```java
@Aop(TransAop.READ_COMMITTED)
```

之所以可用,是因为MainModule中的

```
@IocBy(args={....., "*tx", .....}) // *tx所加载的事务aop
```