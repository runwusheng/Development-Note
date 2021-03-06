# Android Gradle使用

> 全文在windows环境中使用

第一次使用Gradle命令行输入时，需要给gradle配置环境变量，gradle目录可以在android studio中找到，然后把bin配置到windows的环境变量中，这样就可以使用gradle命令了。

### 出现不能下载包的问题

请在Android根目录的`build.gradle`的`repositories`添加下面的aliyun映射的maven地址：

```groovy
 maven { url 'https://maven.aliyun.com/repository/jcenter' }
 maven { url 'https://maven.aliyun.com/repository/google' }
 maven { url 'https://maven.aliyun.com/repository/central' }
 maven { url 'https://maven.aliyun.com/repository/public' }
 maven { url 'https://maven.aliyun.com/repository/gradle-plugin' }
```

### Gradle常用命令
> 在Mac环境中对应将gradle替换成`./gradlew`，**注意：如果在windows中出现`gradle`命令找不到的情况，请使用`gradlew`（gradle的包装工具），如果在`git bash`中无法运行，请尝试在cmd中运行**，或者执行`.\gradlew.bat`

`gradle -v`  # 查看gradle版本

`gradle build`  # 检查依赖并编译打包

`gradle build ----stacktrace`  # 检查依赖并编译打包，打印出编译信息和错误信息

`gradle clean`  # 清除build目录

`gradle assemble`  # 编译并打包apk或aar

`gradle assembleDebug`  #编译并打Debug的apk或aar 

`gradle assembleRelease`  #编译并打Release的apk或aar

`gradle installRelease`  # Release模式打包并安装

`gradle uninstallRelease`  # 卸载Release模式包

`gradle build --scan` #Build Scan

### 传递性依赖

传递性依赖是指引入aar会自动去下载aar中的第三方dependencies。


### Build Variants的使用

具体使用可以查看[官方文档](https://developer.android.com/studio/build/build-variants?hl=zh-cn)


### 源集
* `src/main/`此源集包括所有构建变体共用的代码和资源。
* `src/<buildType>/`创建此源集可加入特定构建类型专用的代码和资源。
* `src/<productFlavor>/`创建此源集可加入特定产品风味专用的代码和资源。
* `src/<productFlavorBuildType>/`创建此源集可加入特定构建变体专用的代码和资源。

    如果不同源集包含同一文件的不同版本，Gradle 将按以下优先顺序决定使用哪一个文件（左侧源集替换右侧源集的文件和设置）：`构建变体 > 构建类型 > 产品风味 > 主源集 > 库依赖项`

### 新版本的更新

`Gradle 3.4` 引入了新的依赖配置，新增了 `api` 和 `implementation` 来代替 `compile` 依赖配置。其中 `api` 和以前的 `compile` 依赖配置是一样的。使用 `implementation` 依赖配置，会显著提升构建时间。
`api`和`implementation`的区别在于`implementation`不会暴露其依赖库给其他引用其本身的工程，简单来说就是可能隐藏内部的依赖库。

如果你是一个lib库的维护者，对于所有需要公开的 API 你应该使用 api 依赖配置，测试依赖或不让最终用户使用的依赖使用 implementation 依赖配置。[Gradle 依赖配置 api VS implementation](https://yuweiguocn.github.io/gradle-new-dependency-configurations/)

### Gradle依赖排除

##### 在dependency中排除

```groovy
implementation('org.jetbrains.anko:anko:0.10.8') {
    exclude group: 'com.android.support'
}
```

##### 强制使用某个版本

```groovy
implementation ('com.android.support:support-v4:28.0.0') {
    force = true
}
```

### 注意

* 如果在Mac系统中运行`./gradlew`出现`gradlew: Permission Denied`的问题，请执行`chmod +x gradlew`
* 当出现`Exception is:
org.gradle.api.GradleScriptException: A problem occurred evaluating root project`错误时，请检查`gradle/wrapper/gradle-wrapper.properties`中的gradle版本是否在在本机安装
* 使用maven.aliyun时，如果出现`Could not GET xxx, Received status code 400 from server: Bad Request`，检查`.gradle/gradle.properties`中是否有代理地址未住释


### 参考
* [配置构建变体](https://developer.android.com/studio/build/build-variants?hl=zh-cn)
* [Gradle 完整指南（Android）](https://juejin.im/entry/57c7a00e0a2b58006b1a1358)
* [Gradle特性](https://segmentfault.com/a/1190000004018407)
* [一文彻底搞清 Gradle 依赖](https://mp.weixin.qq.com/s/1Wl5hEjFAfkjMrJLias-uA)
* [构建神器Gradle](http://jiajixin.cn/2015/08/07/gradle-android/#)
* [Gradle命令详解与导入第三方包](http://stormzhang.com/devtools/2015/01/05/android-studio-tutorial5/)
* [Android Build Variants 为项目设置变种版本](http://blog.csdn.net/mq2553299/article/details/71429657?locationNum=13&fps=1)
* [Android Studio的两种模式及签名配置](http://www.cnblogs.com/details-666/p/keystore.html)
* [How to set versionName in APK filename using gradle?](https://stackoverflow.com/questions/18332474/how-to-set-versionname-in-apk-filename-using-gradle)
* [How to get current buildType in Android Gradle configuration](https://stackoverflow.com/questions/25739163/how-to-get-current-buildtype-in-android-gradle-configuration)
* [gradlew 和 gradle命令的区别](<https://juejin.im/post/5ac9d48d6fb9a028e014bf15>)
* [android studio gradle插件无法下载，Could not GET xxx, Received status code 400 from server: Bad Request](https://blog.csdn.net/lqx_sunhan/article/details/82633275)
