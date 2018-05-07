# ftp下载

## ftp控制

* [FTP任务注解](http://aria.laoyuyu.me/aria_doc/start/annotation_explain.html#httpftp%E5%8D%95%E4%BB%BB%E5%8A%A1%E4%B8%8B%E8%BD%BD%E6%B3%A8%E8%A7%A3)

* 开始\恢复下载
 ```java
 Aria.download(this)
    .loadFtp("ftp://192.18.104.129:21/haha/large.rar")
    .login("lao", "123456")				//登录FTP服务器
    .setFilePath("/mnt/sdcard/")	//设置文件保存文件夹
    .start();
```

* 暂停
 ```java
  Aria.download(this).loadFtp(URL).stop();
 ```

* 删除任务
 ```java
  Aria.download(this).loadFtp(URL).cancel();
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
* FTP下载必须加上端口号
* aria支持读取url中的账号和密码，但是如果url中已经带有账号和密码，则不能使用`login()`进行登录，否则url中的账号密码将被覆盖
* 对于公网上盗版资源的ftp链接，不能保证一定能下载成功，因为这些盗版资源在会经常性被删除。而迅雷之所以能下载，是因为迅雷有自己的资源库，一个链接不通，它可能有另外的链接进行下载