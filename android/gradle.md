
# as修改gradle镜像

```
buildscript {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.3'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        jcenter()
    }
}
```

# gradle 慢解决方法

在使用AS开发安卓应用程序的时候经常会遇到Gradle build running一直在运行甚至卡死的情况，解决方法如下：

- 方法1：

    1、在C:\User\<用户名>\.gradle 目录下新建一个gradle.properties文件，并在里面添加一行：org.gradle.daemon=true
    2、打开AS，在Settings中设置Gradle的工作模式为offline

    这样就可以解决一直在running的问题了

- 方法2：

       找到路径C:\Users\admin\.gradle\wrapper\dists，在此文件夹下有一个gradle版本文件夹，打开后是一个名字很长的文件夹，
    例如我的C:\Users\admin\.gradle\wrapper\dists\gradle-2.4-all\6r4uqcc6ovnq6ac6s0txzcpc0   然后下载对应版本的gradle，将下载的压缩包直接放进名字很长的文件夹中即可，不需要解压

- 方法3：

    需要在android studio 中配置gradle的代理，当然是用goagent了。
    打开setting->gradle->Gradle VM Options：
    -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=8087
    设置生成功后，重启androidstudio ，速度会非常快。

- 方法4：

    1）进入刚安装的Android Studio目录下的bin目录。找到idea.properties文件，用文本编辑器打开。
    2）在idea.properties文件末尾添加一行： disable.android.first.run=true ，然后保存文件。
    3）关闭Android Studio后重新启动，便可进入界面。

```
//开源中国镜像

repositories {       mavenCentral()       jcenter()       mavenLocal()   }

allprojects {    repositories {        maven{ url 'http://maven.oschina.net/content/groups/public/'}    }}
```

## 安装Gradle
gradle官网最新推荐SDKMan安装Gradle：
第一步：打开一个终端安装SDKMAN!

curl -s https://get.sdkman.io | bash
source "/Users/[your username]/.sdkman/bin/sdkman-init.sh"

第二步：新打开一个终端安装你想要的gradle版本
sdk install gradle 3.3
