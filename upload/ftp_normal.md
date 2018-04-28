# FTP单文件上传
* 开始\恢复上传

 ```java
 Aria.upload(this)
 	.loadFtp("/mnt/sdcard/gggg.apk") //上传文件路径
    .setUploadUrl(URL)		//上传的ftp服务器地址
    .login("lao", "123456")
    .start();
 ```

* 暂停

 ```java
  Aria.upload(this).loadFtp(FILE_PATH).stop();
 ```

* 删除任务

 ```java
 Aria.upload(this).loadFtp(FILE_PATH).cancel();
 ```

 * 设置扩展字段
有的时候，你可能希望在下载的时候存放一些自己的数据，这时你可以调用该接口将数据保存下来（如果你数据比较多，或者数据比较复杂，你可以先把数据转换为JSON，然后再将其存到Aria的下载实体中）

  ```java
  Aria.download(this).loadFtp(URL).setExtendField("扩展字段").start();
  ```
  需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
  如下所示：
  ```java
  Aria.download(this).loadFtp(URL).setExtendField("扩展字段").save();
  ```


## 注意事项
* FTP上传需要FTP 服务器给用户打开`write`的权限
* 如果需要支持断点上传，需要FTP服务器给用户打开`append`权限
* FTP下载必须加上端口号
* aria支持读取url中的账号和密码，但是如果url中已经带有账号和密码，则不能使用`login()`进行登录，否则url中的账号密码将被覆盖
