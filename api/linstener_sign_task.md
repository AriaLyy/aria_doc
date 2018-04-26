在Aria中，注解是对应全部任务的，拿onComplete来说，你的下载队列中有3个任务，并且三个任务都已经下载完成，那么onComplete注解就会被调用3次。

这个时候，如果你希望只获取第一个任务A，A的下载地址为（`http://aaa.bbb.zip`）的完成事件，那么，你可以通过`task.getKey().eques("http://aaa.bbb.zip")`来判断当前的comple回调是否是A任务，其它注解同理