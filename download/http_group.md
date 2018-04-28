# http组合任务
任务组的下载和普通任务的下载基本上差不多，区别在于，任务组下载不需要对每一个子任务设置保存路径，**但是需要设置任务组保存文件夹路径，所有子任务都保存在该文件夹下**

* 下载\恢复下载

  ```java
  Aria.download(this)
      .loadGroup(urls)     //设置一主任务，参数为List<String>
      .setDownloadDirPath(groupDirPath)    //设置任务组的文件夹路径
      /**
       * 任务组总任务大小，任务组是一个抽象的概念，没有真实的数据实体，任务组的大小是Aria动态获取子任务大小相加而得到的，
       * 如果你知道当前任务组总大小，你也可以调用该方法给任务组设置大小
       *
       * 为了更好的用户体验，建议直接设置任务组文件大小
       */
      .setFileSize(fileSize) 
      .start();   //启动下载
  ```
* 暂停

  ```java
  Aria.download(this).loadGroup(urls).pause();
  ```

* 取消下载

  ```java
  Aria.download(this).loadGroup(urls).cancel();
  ```

* 设置头部参数
  在任务组中，设置的头部参数将用于所有的子任务
  ```java
   Aria.download(this).loadGroup(urls).addHeader("key", "value").start();
  ```
  需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
  如下所示：
  ```java
  Aria.download(this).loadGroup(urls).addHeader("key", "value").save();
  ```

* 设置扩展字段
有的时候，你可能希望在下载的时候存放一些自己的数据，这时你可以调用该接口将数据保存下来（如果你数据比较多，或者数据比较复杂，你可以先把数据转换为JSON，然后再将其存到Aria的下载实体中）

  ```java
  Aria.download(this).loadGroup(urls).setExtendField("扩展字段").start();
  ```
  需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
  如下所示：
  ```java
  Aria.download(this).loadGroup(urls).setExtendField("扩展字段").save();
  ```