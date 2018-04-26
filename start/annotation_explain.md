## 注意事项
除了在widget（Activity、Fragment、Dialog、Popupwindow）中使用注解方法外，你还可以在Service、Notification等组件中使用注解函数。
 **注意：**
 - 注解回掉采用Apt的方式实现，所以，你不需要担心这会影响你机器的性能
 - 被注解的方法**不能被private修饰**
 - 被注解的方法**只能有一个参数，并且参数类型必须是`DownloadTask`或`UploadTask`或`DownloadGroupTask`**
 - 方法名可以为任意字符串

## HTTP\FTP单任务下载注解
| 注解 | 说明 | 示例 |
| ------| ------ | ------ |
| `@Download.onPre` | 预处理的注解，在任务为开始前回调（一般在此处预处理UI界面） |  `@Download.onPre void onPre(DownloadTask task) {}` |
| `@Download.onTaskStart` | 任务开始时的注解，新任务开始时进行回调 |  `@Download.onTaskStart void taskStart(DownloadTask task) {}`|
| `@Download.onTaskResume` | 任务恢复时的注解，任务从停止恢复到运行前进行回调 | `@Download.onTaskResume void taskResume(DownloadTask task) {}` |
| `@Download.onTaskRunning` | 任务执行时的注解，任务正在执行时进行回调 | `@Download.onTaskRunning void running(DownloadTask task) {}` |
| `@Download.onWait` | 队列已经满了，继续创建新任务，将会回调该方法 | `@Download.onWait void onWait(DownloadTask task){}` |
| `@Download.onTaskStop` | 任务停止时的注解，任务停止时进行回调 | `@Download.onTaskStop void taskStop(DownloadTask task) {}` |
| `@Download.onTaskCancel` | 任务被删除时的注解，任务被删除时进行回调 | `@Download.onTaskCancel void taskCancel(DownloadTask task) {}` |
| `@Download.onTaskFail` | 任务失败时的注解，任务执行失败时进行回调 | `@Download.onTaskFail void taskFail(DownloadTask task) {}` |
| `@Download.onTaskComplete` | 任务完成时的注解，任务完成时进行回调 | `@Download.onTaskComplete void taskComplete(DownloadTask task) {}` |
| `@Download.onNoSupportBreakPoint` | 这是一个特殊的注解，用于处理不支持断点续传的任务 | `@Download.onNoSupportBreakPoint void onNoSupportBreakPoint(DownloadTask task) {}` |


## HTTP组合任务下载\FTP文件夹下载注解
| 注解 | 说明 | 示例 |
| ------| ------ | ------ |
| `@DownloadGroup.onPre` | 预处理的注解，在任务为开始前回调（一般在此处预处理UI界面） |  `@DownloadGroup.onPre void onPre(DownloadGroupTask task) {}` |
| `@DownloadGroup.onTaskStart` | 任务开始时的注解，新任务开始时进行回调 |  `@DownloadGroup.onTaskStart void taskStart(DownloadGroupTask task) {}`|
| `@DownloadGroup.onTaskResume` | 任务恢复时的注解，任务从停止恢复到运行前进行回调 | `@DownloadGroup.onTaskResume void taskResume(DownloadGroupTask task) {}` |
| `@DownloadGroup.onTaskRunning` | 任务执行时的注解，任务正在执行时进行回调 | `@DownloadGroup.onTaskRunning void running(DownloadGroupTask task) {}` |
| `@DownloadGroup.onWait` | 队列已经满了，继续创建新任务，将会回调该方法 | `@DownloadGroup.onWait void onWait(DownloadGroupTask task){}` |
| `@DownloadGroup.onTaskStop` | 任务停止时的注解，任务停止时进行回调 | `@DownloadGroup.onTaskStop void taskStop(DownloadGroupTask task) {}` |
| `@DownloadGroup.onTaskCancel` | 任务被删除时的注解，任务被删除时进行回调 | `@DownloadGroup.onTaskCancel void taskCancel(DownloadGroupTask task) {}` |
| `@DownloadGroup.onTaskFail` | 任务失败时的注解，任务执行失败时进行回调 | `@DownloadGroup.onTaskFail void taskFail(DownloadGroupTask task) {}` |
| `@DownloadGroup.onTaskComplete` | 任务完成时的注解，任务完成时进行回调 | `@DownloadGroup.onTaskComplete void taskComplete(DownloadGroupTask task) {}` |

## 组合任务中子任务注解
| 注解 | 说明 | 示例 |
| ------| ------ | ------ |
| `@DownloadGroup.onSubTaskRunning` | 任务组子任务下载中时回调 | `@DownloadGroup.onSubTaskRunning void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |
| `@DownloadGroup.onSubTaskPre` | 任务组子任务预处理时回调 | `@DownloadGroup.onSubTaskPre void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |
| `@DownloadGroup.onSubTaskStop` | 任务组子任务停止时回调 | `@DownloadGroup.onSubTaskStop void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |
| `@DownloadGroup.onSubTaskStart` | 任务组子任务开始下载时回调 | `@DownloadGroup.onSubTaskStart void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |
| `@DownloadGroup.onSubTaskComplete` | 任务组子任务完成时时回调 | `@DownloadGroup.onSubTaskComplete void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |
| `@DownloadGroup.onSubTaskFail` | 任务组子任务执行失败时回调 | `@DownloadGroup.onSubTaskFail void onSubTaskRunning(DownloadGroupTask groupTask, DownloadEntity subEntity) {}` |

## HTTP\FTP单任务上传注解
| 注解 | 说明 | 示例 |
| ------| ------ | ------ |
| `@Upload.onPre` | 预处理的注解，在任务为开始前回调（一般在此处预处理UI界面） |  `@Upload.onPre void onPre(UploadTask task) {}` |
| `@Upload.onTaskStart` | 任务开始时的注解，新任务开始时进行回调 |  `@Upload.onTaskStart void taskStart(UploadTask task) {}`|
| `@Upload.onTaskResume` | 任务恢复时的注解，任务从停止恢复到运行前进行回调 | `@Upload.onTaskResume void taskResume(UploadTask task) {}` |
| `@Upload.onTaskRunning` | 任务执行时的注解，任务正在执行时进行回调 | `@Upload.onTaskRunning void running(UploadTask task) {}` |
| `@Upload.onWait` | 队列已经满了，继续创建新任务，将会回调该方法 | `@Upload.onWait void onWait(UploadTask task){}` |
| `@Upload.onTaskStop` | 任务停止时的注解，任务停止时进行回调 | `@Upload.onTaskStop void taskStop(UploadTask task) {}` |
| `@Upload.onTaskCancel` | 任务被删除时的注解，任务被删除时进行回调 | `@Upload.onTaskCancel void taskCancel(UploadTask task) {}` |
| `@Upload.onTaskFail` | 任务失败时的注解，任务执行失败时进行回调 | `@Upload.onTaskFail void taskFail(UploadTask task) {}` |
| `@Upload.onTaskComplete` | 任务完成时的注解，任务完成时进行回调 | `@Upload.onTaskComplete void taskComplete(UploadTask task) {}` |


## tip
__TIP：如果你子希望对单个任务，或某一些特定任务设置监听器。__ <br>
可以在注解中添加任务的下载地址，则表示只有该任务才会触发被注解的方法__。

 ```java
 @Download.onTaskRunning({
      "https://test.xx.apk",
      "http://test.xx2.apk"
  }) void taskRunning(DownloadTask task) {
    mAdapter.setProgress(task.getDownloadEntity());
  }
 ```
在上面的例子中，只有下载地址是`https://test.xx.apk`和`http://test.xx2.apk`才会触发
`taskRunning(DownloadTask task)`方法。
除了用注解判断任务外，你还可以使用`task.getKey()`来判断当前任务，`getKey()`返回的是下载地址或上传任务
```java
@Download.onTaskRunning void taskRunning(DownloadTask task) {
   if(task.getKey().eques(DOWNLOAD_URL)){
     mAdapter.setProgress(task.getDownloadEntity());
   }
}
```








