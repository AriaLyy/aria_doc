# 反馈问题
如果在使用Aria的过程中遇到问题，请先在[issues](https://github.com/AriaLyy/Aria/issues)查找，有没有其它小伙伴以前发起的提问。<br>
如果没有的话，在文档中查找有没有相应的说明。<br>
如果还是有问题的话，麻烦在[issues](https://github.com/AriaLyy/Aria/issues)给我留言。<br>
如果你遇到问题，我希望你能在`aria_config.xml`中添加以下配置，然后把log发给我
```
<app>
    <!--是否使用AriaCrashHandler来捕获异常，异常日志保存在：/mnt/sdcard/Android/data/{package_name}/files/log/-->
    <useAriaCrashHandler value="true"/>
    <!--设置Aria的日志级别，{@link ALog#LOG_LEVEL_VERBOSE}-->
    <logLevel value="2"/>
</app>
```
在反馈问题的时候，麻烦尽量描述清楚出bug的步骤，越详细越好。如果你能提供错误日志，那就更好了，这样我才能快速定位问题。<bar>

