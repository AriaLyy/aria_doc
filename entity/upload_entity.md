<!-- ex_nonav -->
## UploadEntity
UploadEntity为上传文件的载体，里面包含了上传文件的一些关键信息

| 字段 | 类型 | 作用 | 备注 |
| :----: | :----: | ---- | ---- |
| speed | long | 速度（单位为：byte）| |
| convertSpeed | String | 转换后的速度（mb/s）| 需要在[config](http://aria.laoyuyu.me/aria_doc/start/config.html)中配置，如果不配置，则为null |
| str | String | 扩展字段 | [扩展字段说明](http://aria.laoyuyu.me/aria_doc/api/extend_field.html) |
| fileSize | long | 文件大小（单位为byte） | |
| convertFileSize | String | 单位转换后的文件大小（xxmb） | 需要在[config](http://aria.laoyuyu.me/aria_doc/start/config.html)中配置，如果不配置，则为null |
| state | int | 状态 | 0：失败；1：完成；2：停止；3：等待；<br> 4：正在执行；5：预处理；6：预处理完成；7：取消任务 |
| currentProgress | long | 当前下载进度（单位为byte） | |
| completeTime | long | 完成时间(时间戳) | |
| percent | int | 进度百分比 | 如：54% |
| isComplete | boolean | 是否已经完成 | true：任务已完成；false：任务未完成 |
| url | String | 文件上传路径 | |
| fileName | String | 文件名 | |
| isGroupChild | boolean | 是否属于组合任务 | true：属于组合任务；false：不属于组合任务 |
| redirectUrl | String | 重定向地址 | 如果任务没有发生重定向，则为null |
| isRedirect | boolean | 是否重定向 | true：已经重定向；false：没有重定向 |
| filePath | String | 上传的文件路径 | 保存路径是唯一的 |
| responseStr | String | 上传完成后服务器返回的数据 | |