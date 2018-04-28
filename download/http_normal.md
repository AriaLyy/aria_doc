
# 普通任务操作

* 下载\恢复下载

  ```java
  Aria.download(this)
      .load(DOWNLOAD_URL)     //读取下载地址
      .setDownloadPath(DOWNLOAD_PATH)    //设置文件保存的完整路径
      .setRequestMode(RequestEnum.POST)		// 设置请求类型
      .start();   //启动下载
  ```
* 暂停

  ```java
  Aria.download(this).load(DOWNLOAD_URL).pause();
  ```

* 取消下载

  ```java
  Aria.download(this).load(DOWNLOAD_URL).cancel();
  ```

* 设置头部参数

  ```java
   Aria.download(this).load(DOWNLOAD_URL).addHeader("key", "value").start();
  ```
  需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
  如下所示：
  ```java
  Aria.download(this).load(DOWNLOAD_URL).addHeader("key", "value").save();
  ```

* 设置扩展字段
有的时候，你可能希望在下载的时候存放一些自己的数据，这时你可以调用该接口将数据保存下来（如果你数据比较多，或者数据比较复杂，你可以先把数据转换为JSON，然后再将其存到Aria的下载实体中）

  ```java
  Aria.download(this).load(DOWNLOAD_URL).setExtendField("扩展字段").start();
  ```
  需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
  如下所示：
  ```java
  Aria.download(this).load(DOWNLOAD_URL).setExtendField("扩展字段").save();
  ```