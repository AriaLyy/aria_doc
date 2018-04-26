## FtpUrlEntity

| 字段 | 类型 | 作用 | 备注 |
| :----: | :----: | ---- | ---- |
| remotePath | String | 远程路径 | 如：`ftp://127.0.0.1:21/download/AriaPrj.zip`<br> remetePath便是：`download/AriaPrj.zip`|
| account | String | 账号 | |
| url | String | 原始url | |
| protocol | String | ftp协议 | ftp |
| user | String | 登录的用户名 | |
| password | String | 登录密码 | |
| port | String | 端口 | |
| hostName | String | 主机域名 | |
| needLogin | boolean | 是否需要登录 | true：需要；false：不需要 |
| validAddr | InetAddress | 有效的主机地址 | |