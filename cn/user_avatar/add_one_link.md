# 建立关联关系

## 好了,这里是第一次用到NutDao的关联关系了, 打开User类,加入2行

```java
	@One(target=UserProfile.class, field="id", key="userId")
	protected UserProfile profile;
```

### 自然的,为其添加Getter/Setter
