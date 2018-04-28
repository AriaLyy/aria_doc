<!-- ex_nonav -->
## DownloadGroupTaskEntity
DownloadGroupTaskEntity为HTTP组合任务\FTPdir文件夹任务信息

| 字段 | 类型 | 作用 | 备注 |
| :----: | :----: | ---- | ---- |
| state | int | 任务状态 | 0：失败；1：完成；2：停止；3：等待；<br> 4：正在执行；5：预处理；6：预处理完成；7：取消任务 |
| headers | Map<String, String> | 请求头信息 | 只有http类任务才有 |
| charSet | String | 字符编码 | 默认为"utf-8" |
| requestEnum | RequestEnum | 请求类型 | `GET`、`POST` |
| redirectUrl | String | 重定向地址 | http任务发生重定向才有 |
| removeFile | boolean | 删除任务时，是否删除已下载完成的文件 | true： 删除任务数据库记录，并且删除已经下载完成的文件<br> false：如果任务已经完成，只删除任务数据库记录 <br> 未完成的任务，不管true还是false，都会删除文件|
| code | int | http状态码 | |
| urlEntity | [FtpUrlEntity](http://aria.laoyuyu.me/aria_doc/entity/ftp_url_entity.html) | ftp登录信息 | 只有ftp任务才有 |
| entity | [DownloadGroupEntity](http://aria.laoyuyu.me/aria_doc/entity/group_entity.html) | http组合任务\ftp_dir任务实体 | |
| subTaskEntities | List<[DownloadTaskEntity](http://aria.laoyuyu.me/aria_doc/entity/download_task_entity.html)> | 对应的下载任务的任务实体 |
