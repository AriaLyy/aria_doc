### 停止所有正在下载的任务
停止所有任务的命令，并清空所有等待队列
```java
Aria.download(this).stopAllTask();
或
Aria.upload(this).stopAllTask();
```

### 恢复所有停止的任务
1. 如果执行队列没有满，则开始下载任务，直到执行队列满
2. 如果队列执行队列已经满了，则将所有任务添加到等待队列中
```java
Aria.download(this).resumeAllTask();
或
Aria.upload(this).resumeAllTask();
```

### 删除所有任务
```java
Aria.download(this).removeAllTask();
或
Aria.upload(this).removeAllTask();
```
1. 如果任务为完成，会删除没有完成的文件</br> 
2. 如果使用`removeAllTask(true)`方法，会将已经下载完成和未完成的文件删除</br> 
3. 如果是上传任务，不会删除本地的上传文件，但如果使用`removeAllTask(true)`，同样会删除本地上传文件

### 获取任务当前状态
```java
Aria.download(this).getTaskState();
或
Aria.upload(this).getTaskState();
```
| 状态码 | 说明 |
| :----: | :----: |
| -1 | 未知状态 |
| 0 | 失败 |
| 1 | 成功 |
| 2 | 停止 |
| 3 | 等待 |
| 4 | 执行中 |
| 5 | 预处理 |
| 6 | 预处理完成 |
| 7 | 删除任务 |

### 删除单个任务
```java
/**
 * 删除任务
 *
 * @param removeFile {@code true} 不仅删除任务数据库记录，还会删除已经删除完成的文件
 * {@code false}如果任务已经完成，只删除任务数据库记录，
 */
Aria.download(this).cancel(true);
或
Aria.upload(this).cancel(true);
```



### 重置任务状态
状态重置之后，任务将重新开始执行
```java
Aria.download(this).resetState();
或
Aria.upload(this).resetState();
```


### 修改文件保存信息
设置文件存储路径，如果需要修改新的文件名，修改路径便可。<br>
如：原文件路径 /mnt/sdcard/test.zip<br>
如果需要将test.zip改为game.zip，只需要重新设置文件路径为：/mnt/sdcard/game.zip
```java
Aria.download(this).load(DOWNLOAD_URL).setDownloadPath(newPath);
```

### 设置队列最大任务数
```java
Aria.get(this).getDownloadConfig().setMaxTaskNum(3);
或
Aria.get(this).getUploadConfig().setMaxTaskNum(3);
```

### 设置最大下载速度
制单个任务的上传、下载的最大速度（单位为 kb）
```java
Aria.download(this).setMaxSpeed(speed);
```


### 最高优先级任务
```java
Aria.download(this).load(DOWNLOAD_URL)`<br>`.setDownloadPath(PATH).setHighestPriority();
```
将任务设置为最高优先级任务，最高优先级任务有以下特点：<br>
1、在下载队列中，有且只有一个最高优先级任务<br> 
2、最高优先级任务会一直存在，直到用户手动暂停或任务完成<br>
3、任务调度器不会暂停最高优先级任务<br>
4、用户手动暂停或任务完成后，第二次重新执行该任务，该命令将失效<br>
5、如果下载队列中已经满了，则会停止队尾的任务，当高优先级任务完成后，该队尾任务将自动执行<br>
6、把任务设置为最高优先级任务后，将自动执行任务，不需要重新调用start()启动任务

### 设置请求类型
```java
Aria.download(this).load("").setRequestMode(RequestEnum.GET);
或
Aria.upload(this).load("").setRequestMode(RequestEnum.GET);
```

### 删除下载记录
* 第一种删除方式
```java
Aria.download(this).load(url).removeRecord();
或
Aria.upload(this).load(url).removeRecord();
```
* 第二种删除方式
```java
/**
 * 删除任务记录
 *
 * @param type 需要删除的任务类型，1、表示单任务下载。2、表示任务组下载。3、单任务上传
 * @param key 下载为保存路径、任务组为任务组名、上传为上传文件路径
 */
Aria.get(this).delRecord(type, key);
```

### 获取任务实体
* HTTP\FTP单任务下载实体
```java
DownloadEntity entity = Aria.download(this).getDownloadEntity(DOWNLOAD_URL);
```
* HTTP任务组\FTP文件夹实体
```java
DownloadGroupTaskEntity entity = Aria.download(this).getDownloadGroupTask(mUrls);
```
* HTTP\FTP单任务上传实体
```java
UploadEntity entity = Aria.upload(this).getUploadEntity(FILE_PATH);
```

### 获取下载的文件大小、当前进度百分比
同样的，你也可以在DownloadTask对象中获取下载的文件大小
```java
@Override public void onTaskRunning(DownloadTask task) {
  //获取任务文件实体（里面包含文件名，下载地址，保存路径等信息）
  DownloadEntity entity = task.getEntity();
  //获取文件大小
  long fileSize = task.getFileSize();
  //获取单位转换后的文件大小
  String fileSize1 = task.getConvertFileSize();
  //当前进度百分比
  int percent = task.getPercent();
}
```

### 获取当前任务的下载速度
``` java
@Override public void onTaskRunning(DownloadTask task) {
  //如果你打开了速度单位转换配置，将可以通过以下方法获取带单位的下载速度，如：1 mb/s
  String convertSpeed = task.getConvertSpeed();
  //如果你有自己的单位格式，可以通过以下方法获取原始byte长度
  long speed = task.getSpeed();
}
```

### 设置头参数
对于某些服务器，需要通过添加headler参数才能和服务器进行交互，如果你需要对任务增加header支持，那么你可以
* 添加一个headler参数
 ```java
  Aria.download(this)
    .load(DOWNLOAD_URL, true)
    .addHeader("key", "value")
    .save();
 ``` 
* 添加一组headler参数
 ```java
 Aria.download(this)
    .load(DOWNLOAD_URL, true)
    .addHeaders(headlerMap)
    .save();
 ```
 需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
如下所示：
```java
  Aria.download(this).loadFtp(URL).addHeader("key", "value").save();
```

### 使用服务端提供的文件名

在某些场景下，可能需要使用服务端提供的文件名，那么你可以这么做

```java

 Aria.download(SingleTaskActivity.this)
        .load(DOWNLOAD_URL)
        .useServerFileName(true)  // 使用服务端提供的文件名
        .setRequestMode(RequestEnum.GET)
        .setFilePath(Environment.getExternalStorageDirectory().getPath() + "/ggsg3.apk")
        .start();
```

需要注意的是，Aria是从服务器端的`content-disposition`字段获取文件名，`content-disposition`对应的value的数据格式必须如下所示，否则获取不到文件名
```
attachment;filename=xxx  // xxx 为文件名
```

