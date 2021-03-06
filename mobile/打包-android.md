

# allowBackup 安全风险

- Android API Level 8 及其以上 Android 系统提供了为应用程序数据的备份和恢复功能，此功能的开关决定于该应用程序中 AndroidManifest.xml 文件中的 allowBackup 属性值，其属性值默认是 True。当 allowBackup 标志为 true 时，用户即可通过 adb backup 和 adb restore 来进行对应用数据的备份和恢复，这可能会带来一定的安全风险。

  Android 属性 allowBackup 安全风险源于 adb backup 容许任何一个能够打开 USB 调试开关的人从Android 手机中复制应用数据到外设，一旦应用数据被备份之后，所有应用数据都可被用户读取；adb restore 容许用户指定一个恢复的数据来源（即备份的应用数据）来恢复应用程序数据的创建。因此，当一个应用数据被备份之后，用户即可在其他 Android 手机或模拟器上安装同一个应用，以及通过恢复该备份的应用数据到该设备上，在该设备上打开该应用即可恢复到被备份的应用程序的状态。

  尤其是通讯录应用，一旦应用程序支持备份和恢复功能，攻击者即可通过 adb backup 和 adb restore 进行恢复新安装的同一个应用来查看聊天记录等信息；对于支付金融类应用，攻击者可通过此来进行恶意支付、盗取存款等；因此为了安全起见，开发者务必将 allowBackup 标志值设置为 false 来关闭应用程序的备份和恢复功能，以免造成信息泄露和财产损失。

- 在 AndroidManifest.xml 文件显示设置 allowBackup 属性值为 false，即 android:allowBackup="false"，如

  ```
    <application
                android:allowBackup="false"
      ...
  ```

# Manifest文件设置debug属性

- 只有android:debuggable="true"时我们才可以在手机上调试Android程序。
  但是当我们没在AndroidManifest.xml中设置其debug属性时:
  使用Eclipse运行这种方式打包时其debug属性为true,使用Eclipse导出这种方式打包时其debug属性为法false.
  在使用ant打包时，其值就取决于ant的打包参数是release还是debug.

  因此在AndroidMainifest.xml中最好不设置android:debuggable属性值，而是由打包方式来决定其值。

  从这里我们可以看出，假如反编译别人的apk之后，想要看别人的打印log，只需要在manifest文件中加上debug为true重新打打包就可以了哦。

# 关闭webview组件的保存密码功能

    在SystemWebViewEngine.java init方法中加入如下代码

    ```
        webView.getSettings().setSavePassword(false);
    ```

# 代码混淆

1. 在build.gradle的buildTypes中加入

```
    debug {
       debuggable true
    }
    release {
        // Zipalign优化
        zipAlignEnabled true
        // 移除无用的resource文件
        shrinkResources true
        // 去掉debug
        debuggable false
        // 混淆
        minifyEnabled true
        // 混淆规则
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        signingConfig signingConfigs.release
    }
```

2. 复制proguard-rules.txt到android根目录下,该文件是通用的混淆规则。

# 组件导出

- android:exported 是Android中的四大组件 Activity，Service，Provider，Receiver 四大组件中都会有的一个属性。

  总体来说它的主要作用是：是否支持其它应用调用当前组件。

  默认值：如果包含有intent-filter 默认值为true; 没有intent-filter默认值为false。
