
# Plugin with id 'android-library' not found

添加如下代码到 Gradle build file:
```
buildscript {
    repositories {
        jcenter()
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        google()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'
    }
}
```