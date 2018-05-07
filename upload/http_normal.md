# http上传

## 任务控制

* [事件注解](http://aria.laoyuyu.me/aria_doc/start/annotation_explain.html#httpftp%E5%8D%95%E4%BB%BB%E5%8A%A1%E4%B8%8A%E4%BC%A0%E6%B3%A8%E8%A7%A3)

* 添加任务(只添加，不上传)

 ```java
 Aria.upload(this)
     .load(filePath)     //文件路径
     .setDownloadPath(DOWNLOAD_PATH)    //设置文件保存的完整路径
     .setUploadUrl(uploadUrl)  //上传路径
     .setAttachment(fileKey)   //服务器读取文件的key
     .add();
 ```

* 上传

 ```java
 Aria.upload(this)
     .load(filePath)     //文件路径
     .setUploadUrl(uploadUrl)  //上传路径
     .setAttachment(fileKey)   //服务器读取文件的key
     .start();
 ```
* 取消上传

 ```java
  Aria.upload(this).load(filePath).cancel();
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


## 注意事项
由于HTTP的特性，没法实现一个通用的断点上传方式，因此HTTP上传不支持暂停，每次调用`start()`方法都会重新执行

如果你需要在上传文件的时候获取服务器返回的数据，那么你可以在`onTaskComplete`注解中通过实体`getResponseStr()`获取返回数，如下所示：
```java
@Upload.onTaskComplete public void taskComplete(UploadTask task) {
    L.d(TAG, "上传完成");
    L.d(TAG, "上传成功返回数据（如果有的话）：" + task.getEntity().getResponseStr());
}
```