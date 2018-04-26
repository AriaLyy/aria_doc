## DownloadGroupEntity
DownloadGroupEntity为组合任务的载体，里面包含了组合任务的一些关键信息

| 字段 | 类型 | 作用 | 备注 |
| :----: | :----: | ---- | ---- |
| speed | long | 速度（单位为：byte）| |
| convertSpeed | String | 转换后的速度（mb/s）| 需要在[config]()中配置，如果不配置，则为null |
| str | String | 扩展字段 | [扩展字段说明]() |
| fileSize | long | 文件大小（单位为byte） | |
| convertFileSize | String | 单位转换后的文件大小（xxmb） | 需要在[config]()中配置，如果不配置，则为null |
| state | int | 状态 | 0：失败；1：完成；2：停止；3：等待；<br> 4：正在执行；5：预处理；6：预处理完成；7：取消任务 |
| currentProgress | long | 当前下载进度（单位为byte） | |
| completeTime | long | 完成时间(时间戳) | |
| percent | int | 进度百分比 | 如：54% |
| isComplete | boolean | 是否已经完成 | true：任务已完成；false：任务未完成 |
| groupName | String | 组合任务名 | 为所有子任务url相加的Md5 |
| alias | String | 组合任务别名 | |
| urls | List<String> | 所有的子任务地址 | |
| dirPath | String | 组合任务的保存文件夹 | |
| subEntities | [DownloadEntity]() | 任务实体列表 | |