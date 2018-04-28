# 开始
## 导入aria
在app目录下的build.gradle文件中添加以下依赖
```java
compile 'com.arialyy.aria:aria-core:3.4'
annotationProcessor 'com.arialyy.aria:aria-compiler:3.4'
```
如果出现android support，请将 `compile 'com.arialyy.aria:aria-core:<last-version>'`替换为
```
compile('com.arialyy.aria:aria-core:<last-version>'){
   exclude group: 'com.android.support'
}
```
如果你使用的是kotlin，请使用kotlin官方提供的方法配置apt，[kotlin kapt官方配置传送门](https://www.kotlincn.net/docs/reference/kapt.html)

## 在AndroidManifest文件中添加相应权限
由于Aria涉及到文件和网络的操作，因此需要你在manifest文件中添加以下权限，如果你希望在6.0以上的系统中使用Aria，那么你需要动态向安卓系统申请文件系统读写权限，[如何使用安卓系统权限](https://developer.android.com/training/permissions/index.html?hl=zh-cn)
```xml
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

## 注册aria
在Activity的onCreate、fragment的onCreate、java的构造函数中使用`Aria.download(this).register();`便可以实现注册。
如在activity中：
```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Aria.download(this).register();
}
```

## 启动任务
```java
  Aria.download(this)
      .load(DOWNLOAD_URL)     //读取下载地址
      .setDownloadPath(DOWNLOAD_PATH) //设置文件保存的完整路径
      .start();   //启动下载
```

## 接受任务回调
基于解耦合的考虑，Aria的下载功能是和状态获取相分离的，状态的获取并不会集成到链式代码中，但是Aria提供了另一种更简单更灵活的方案。
通过注解，你可以很容易获取任务的所有状态。
```java
//在这里处理任务执行中的状态，如进度进度条的刷新
@Download.onTaskRunning protected void running(DownloadTask task) {
    if(task.getUrl().eques(url)){
        ....
        可以通过url判断是否是指定任务的回调
    }
    int p = task.getPercent();  //任务进度百分比
    String speed = task.getConvertSpeed();  //转换单位后的下载速度，单位转换需要在配置文件中打开
    String speed1 = task.getSpeed(); //原始byte长度速度
}

@Download.onTaskComplete void taskComplete(DownloadTask task) {
    //在这里处理任务完成的状态
}
```

 **注意：**
 - 注解回掉采用Apt的方式实现，所以，你不需要担心这会影响你机器的性能
 - 被注解的方法**不能被private修饰**
 - 被注解的方法**只能有一个参数，并且参数类型必须是`DownloadTask`或`UploadTask`或`DownloadGroupTask`**
 - 方法名可以为任意字符串
