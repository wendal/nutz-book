# 上传头像的入口方法

## 在UserProfileModule中新增一个方法,带适配器的哦

```java
	@AdaptBy(type=UploadAdaptor.class, args={"${app.root}/WEB-INF/tmp/user_avatar", "8192", "utf-8", "20000", "102400"})
	@POST
	@Ok(">>:/user/profile")
	@At("/avatar")
	public void uploadAvatar(@Param("file")TempFile tf,
			@Attr(scope=Scope.SESSION, value="me")int userId,
			AdaptorErrorContext err) {
		String msg = null;
		if (err != null && err.getAdaptorErr() != null) {
			msg = "文件大小不符合规定";
		} else if (tf == null) {
			msg = "空文件";
		} else {
			UserProfile profile = get(userId);
			try {
				BufferedImage image = Images.read(tf.getFile());
				image = Images.zoomScale(image, 128, 128, Color.WHITE);
				Images.writeJpeg(image, tf.getFile(), 0.8f);
				profile.setAvatar(new SimpleBlob(tf.getFile()){
					public byte[] getBytes(long pos, int length) throws SQLException {
						if (pos == 1 && length == length())
							try {
								return Streams.readBytes(getBinaryStream());
							} catch (IOException e) {
							}
						return super.getBytes(pos, length);
					}
				});
				dao.update(profile, "^avatar$");
			} catch(DaoException e) {
				log.info("System Error", e);
				msg = "系统错误";
			} catch (Throwable e) {
				msg = "图片格式错误";
			}
		}
		
		if (msg != null)
			Mvcs.getHttpSession().setAttribute("upload-error-msg", msg);
	}
```

### 基本步骤是: 先判断是否有上传异常,然后解析图片,缩放,保存到数据库.
### 在编写的过程中,发现SimpleBlob不兼容最新驱动的样子,所以就继承一下,覆盖原本的错误实现.
### Upload适配器的几个参数: 临时文件夹路径,缓存环的大小,编码,临时文件夹的文件数,上传文件的最大大小