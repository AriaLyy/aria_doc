## 获取任务列表

### 下载
* 获取所有普通下载任务，包括已完成和为完成的普通任务
  ```java
  List<DownloadEntity> list = Aria.download(this).getTaskList();
  ```
* 获取所有未完成的普通下载任务
  ```java
  List<DownloadEntity> list = Aria.download(this).getAllNotCompletTask();
  ```
* 获取所有已经完成的普通任务
  ```java
 List<DownloadEntity> list = Aria.download(this).getAllCompleteTask();
  ```
* 获取组合任务列表
  ```java
  List<DownloadGroupEntity> group = Aria.download(this).getGroupTaskList();
  ```
* 获取所有任务的任务列表
  ```java
  List<AbsEntity> list = Aria.download(this).getTotalTaskList();
  ```


### 上传
* 获取所有普通下载任务，包括已完成和为完成的普通任务
  ```java
  List<UploadEntity> list = Aria.upload(this).getTaskList();
  ```
* 获取所有未完成的普通下载任务
  ```java
  List<UploadEntity> list = Aria.upload(this).getAllNotCompletTask();
  ```
* 获取所有已经完成的普通任务
  ```java
 List<UploadEntity> list = Aria.upload(this).getAllCompleteTask();
  ```