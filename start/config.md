## Aria参数配置
在Aria中，你可以在配置文件或调用Aria代码配置Aria的参数。

## 配置文件设置参数
创建`aria_config.xml` 文件，将其放在`assets`目录下
```xml
<?xml version="1.0" encoding="utf-8"?>
<aria>

  <app>
    <!--是否使用AriaCrashHandler来捕获异常，异常日志保存在：/mnt/sdcard/Android/data/{package_name}/files/log/-->
    <useAriaCrashHandler value="true"/>
    <!--设置Aria的日志级别，{@link ALog#LOG_LEVEL_VERBOSE}-->
    <logLevel value="2"/>
  </app>

  <!--注意，修改该配置文件中的属性会覆盖代码中所设置的属性-->
  <download>

    <!--设置下载线程，线程下载数改变后，新的下载任务才会生效，如果任务大小小于1m，该设置也不会生效-->
    <threadNum value="3"/>

    <!--设置下载队列最大任务数， 默认为2-->
    <maxTaskNum value="2"/>

    <!--设置下载失败，重试次数，默认为10-->
    <reTryNum value="2"/>

    <!--设置重试间隔，单位为毫秒，默认2000毫秒-->
    <reTryInterval value="5000"/>

    <!--设置url连接超时时间，单位为毫秒，默认5000毫秒-->
    <connectTimeOut value="5000"/>

    <!--设置IO流读取时间，单位为毫秒，默认20000毫秒，该时间不能少于10000毫秒-->
    <iOTimeOut value="10000"/>

    <!--设置写文件buff大小，该数值大小不能小于2048，数值变小，下载速度会变慢-->
    <buffSize value="8192"/>

    <!--设置https ca 证书信息；path 为assets目录下的CA证书完整路径，name 为CA证书名-->
    <ca name="" path=""/>

    <!--是否需要转换速度单位，转换完成后为：1b/s、1kb/s、1mb/s、1gb/s、1tb/s，如果不需要将返回byte长度-->
    <convertSpeed value="true"/>

    <!--执行队列类型，见com.arialyy.aria.core.QueueMod，默认类型为wait-->
    <queueMod value="wait"/>

    <!--进度更新更新间隔，默认1000毫秒-->
    <updateInterval value="1000"/>

  </download>

  <upload>
    <!--是否需要转换速度单位，转换完成后为：1b/s、1kb/s、1mb/s、1gb/s、1tb/s，如果不需要将返回byte长度-->
    <convertSpeed value="true"/>

    <!--设置上传队列最大任务数， 默认为2-->
    <maxTaskNum value="2"/>

    <!--设置上传失败，重试次数，默认为10-->
    <reTryNum value="2"/>

    <!--设置重试间隔，单位为毫秒-->
    <reTryInterval value="2000"/>

    <!--设置url连接超时时间，单位为毫秒，默认5000毫秒-->
    <connectTimeOut value="5000"/>

    <!--执行队列类型，见com.arialyy.aria.core.QueueMod，默认类型为wait-->
    <queueMod value="wait"/>

    <!--进度更新更新间隔，默认1000毫秒-->
    <updateInterval value="1000"/>
  </upload>

</aria>
```

## 代码中设置参数
除了文件方式外修改Aria参数外，同样的，你也可以在代码中动态修改Aria参数</br>
通过`Aria.get(this).getDownloadConfig()`或`Aria.get(this).getUploadConfig()`直接获取配置文件，然后修改参数</br>
如以下所示：
```java
// 修改最大下载数，调用完成后，立即生效
// 如当前下载任务数是4，修改完成后，当前任务数会被Aria自动调度任务数
Aria.get(this).getDownloadConfig().setMaxTaskNum(3);
```

## 一些参数说明
### 执行队列类型
* wait模式
 队列模式为等待模式。</br>
 当正在执行的任务数已经达到队列设置的最大任务数时，继续下载新任务，Aria则会把新任务缓存到缓存队列中
* now模式
 队列模式为优先下载模式。</br>
 当正在执行的任务数已经达到队列设置的最大任务数时，继续下载新任务，Aria会停止执行队列中的队首任务，新任务会立刻下载

### 设置最大任务数说明（Wait模式下的说明）
* 如果你在下载任务中最大任务数设置为3
  - 当你连续下载的任务数小于3，任务会自动执行
  - 当正在执行的任务有3个时，如果你继续开始新任务，Aria则会将新任务存放在缓存队列中
  - 当正在执行的任务数有3个时，并且缓存队列中有1个任务，这时，如果你调用`setMaxTaskNum(4);`接口将最大任务数设置为4，则Aria会自动执行缓存队列中的任务，直到正在执行的任务数达到最大任务数为止
  - 如果正在执行的任务数有3个，这时，如果你调用`setMaxTaskNum(2);`接口将最大任务数设置为2，那么Aria会自动停止正在执行的队列中的第一个任务。

* 在Aria中，上传任务和下载任务的最大任务数相互独立，互不影响的。
如：在上传类型的任务中，设置的最大的上传任务数为2，同时设置的最大下载任务为4。那么在下载队列中连续打开4个任务也不会暂停任何一个上传任务。
