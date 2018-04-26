# 注解无效、ProxyClassCounter文件未生成
 1. 检查下你的工程中有没有使用apply plugin: 'android-apt'，如果有的话将其转换为annotationProcessor。
 2. 检查下annotationProcessor 和 compile 版本是否一致，不一致的话对导致生成代理文件失败
 3. 如果你是Android studio的module中引用的Aria，那么你还需要再app模块中添加同样的导入代码
    ```gradle
     compile 'com.arialyy.aria:aria-core:{version code}'
     annotationProcessor 'com.arialyy.aria:aria-compiler:{version code}'
    ```
 4. 如果以上设置都无效或控制台打印下面的错误
    ```gradle
    Annotation processors must be explicitly declared now.  The following dependencies on the compile classpath are found to 
    contain annotation processor.  Please add them to the annotationProcessor configuration.
    ```

    请在app的build.gradle文件的defaultConfig块中添加以下代码
    ```gradle
    android {
      compileSdkVersion 26
      buildToolsVersion "26.0.2"
      defaultConfig {
        ....
        javaCompileOptions {
          annotationProcessorOptions {
            includeCompileClasspath true
          }
        }
      }
      ...
    }
    ```
 5. 如果都不是的话，build文件时，点击as右下角的gradle console窗口，看看报什么错误（如果有错误，可以的话，麻烦在Issues留言给我）