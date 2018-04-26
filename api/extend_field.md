### 保存扩展字段
有的时候，你可能希望在下载的时候存放一些自己的数据，这时你可以调用该接口将数据保存下来（如果你数据比较多，或者数据比较复杂，你可以先把数据转换为**JSON**，然后再将其存到Aria的下载实体中）
```java
Aria.download(this).load(DOWNLOAD_URL).setExtendField(str);
或
Aria.upload(this).load(DOWNLOAD_URL).setExtendField(str);
```

### 读取扩展字段
```java
Aria.download(this).load(DOWNLOAD_URL).getExtendField();
或
Aria.upload(this).load(DOWNLOAD_URL).getExtendField();
```

### 注意事项
需要注意的是：如果你没有调用`start()`，`stop()`等操作方法，那么你需要调用`save()`才能将头部数据保存进数据库。
如下所示：
```java
  Aria.download(this).loadFtp(URL).setExtendField("扩展字段").save();
```