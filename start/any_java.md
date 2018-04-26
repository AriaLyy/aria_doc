## 在任意java类中使用aria
从3.4版本开始，Aria支持在任意java类中使用

## 初始化Aria
在Application调用Aria的初始化方法。
```java
 Aria.init(this);
```

## 在module类的构造函数中注册Aria
```java
Aria.download(this).register();
```

## 注意事项
在Activity销毁时需要在modlue中调用`unRegister`销毁事件。
如果不进行销毁操作，将会导致内存泄露！！
```java
Aria.download(this).unRegister();
```


## demo
```java
public class AnyRunnModule {
  String TAG = "AnyRunnModule";
  private Context mContext;
  private String mUrl;

  public AnyRunnModule(Context context) {
    Aria.download(this).register();
    mContext = context;
  }

  @Download.onWait void onWait(DownloadTask task) {
    Log.d(TAG, "wait ==> " + task.getDownloadEntity().getFileName());
  }

  @Download.onPre protected void onPre(DownloadTask task) {
    Log.d(TAG, "onPre");
  }

  @Download.onTaskStart void taskStart(DownloadTask task) {
    Log.d(TAG, "onStart");
  }

  @Download.onTaskRunning protected void running(DownloadTask task) {
    Log.d(TAG, "running");
  }

  @Download.onTaskResume void taskResume(DownloadTask task) {
    Log.d(TAG, "resume");
  }

  @Download.onTaskStop void taskStop(DownloadTask task) {
    Log.d(TAG, "stop");
  }

  @Download.onTaskCancel void taskCancel(DownloadTask task) {
    Log.d(TAG, "cancel");
  }

  @Download.onTaskFail void taskFail(DownloadTask task) {
    Log.d(TAG, "fail");
  }

  @Download.onTaskComplete void taskComplete(DownloadTask task) {
    L.d(TAG, "path ==> " + task.getDownloadEntity().getDownloadPath());
    L.d(TAG, "md5Code ==> " + CommonUtil.getFileMD5(new File(task.getDownloadPath())));
  }


  void start(String url) {
    mUrl = url;
    Aria.download(this)
        .load(url)
        .addHeader("Accept-Encoding", "gzip, deflate")
        .setRequestMode(RequestEnum.GET)
        .setFilePath(Environment.getExternalStorageDirectory().getPath() + "/ggsg1.apk")
        .resetState()
        .start();
  }

  void stop() {
    Aria.download(this).load(mUrl).stop();
  }

  void cancel() {
    Aria.download(this).load(mUrl).cancel();
  }

  void unRegister() {
    Aria.download(this).unRegister();
  }
}
```