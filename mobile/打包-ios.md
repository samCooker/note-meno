# ios设置权限说明

- 未设置权限,app上传失败. ![详情](/mobile/res/ios-app-权限.png '')

# ios日期插件

  js "cn_ZH"


# 极光推送问题

- IOS收不到推送

  JPushConfig.plist文件中,设置isProduction字段为true


  做如下检查：

  找到 TARGET -> Capabilities -> Push Notification 选项点开
  找到 TARGET -> Build Setting -> Code Signing Identity -> Code Signing Entitlements *****Entitle-release.plist 看看有没有 aps-environment 字段，没有补上
  <plist version="1.0">
  <dict>
  	<key>aps-environment</key>
  	<string>development</string>
  </dict>
  </plist>
