
# 手动添加插件

- ios

1. 修改ios.json文件

在
```
"config_munge": {
        "files": {
            "config.xml": {
                "parents": {
                    "/*": [
                        ...
```
中添加
```
{
    "xml": "<feature name=\"xxx1\"><param name=\"ios-package\" value=\"xxx2\" /></feature>",
    "count": 1
}
```
xxx1对应plugin.xml中`js-module`标签的name,xxx2对应`platform >config-file >feature ><param name="ios-package" value="LSFileViewer2"/>`的value

2. 修改cordova_plugins.js

在 module.exports 添加

```
{
    "id": "(插件id).(plugin.xml 中js-module 的name)",
    "file": "plugins/(js文件路径)",
    "pluginId": "(plugin.xml 中的插件id)",
    "clobbers": [
        "(plugin.xml 中的clobbers target)"
    ]
}
```

3. 复制www文件到www/plugins/插件文件夹/

4. 复制src/ios 到 项目id/Plugins/插件文件夹/
