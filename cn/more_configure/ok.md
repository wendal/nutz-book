# 默认@Ok

## 这个项目以json交互为主,所以,默认用json视图好了. 打开MainModule,加入代码

```java
@Ok("json:full")
```

### 这里的json指UTF8JsonView类, 后面的full是JsonFormat的其中一种内置格式的缩写