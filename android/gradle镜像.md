
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

```
//开源中国镜像

repositories {       mavenCentral()       jcenter()       mavenLocal()   }

allprojects {    repositories {        maven{ url 'http://maven.oschina.net/content/groups/public/'}    }}
```