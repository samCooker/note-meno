
* [install](#install)
* [update](#update)
* [关于图标和图片](#关于图标和图片)

# install

- 命令安装

    指令：`npm install -g ionic`

    清空缓存：`npm cache clean`


# update

- ionic 更新

    指令：`npm install -g ionic`

- 项目更新

    v1版本，修改 ionic.project 文件名成 ionic.config.json

    运行 `npm install --save-dev --save-exact @ionic/cli-plugin-cordova@latest` 和 `cnpm install --save-dev --save-exact @ionic/cli-plugin-ionic1@latest` (关于cnpm的安装见npm说明)

# 关于图标和图片

- 1.将图片文件（文件名字必须为splash.png, splash.psd 或 splash.ai）和图标（文件名称必须为icon.png, icon.psd 或 icon.ai）放在resources文件夹下。

    图片尺寸最好是2208x2208 px，图标尺寸最好是1200x1200 px

- 2.使用命令`ionic resources`可以生成不同屏幕尺寸的图片和图标。由于网络的原因，可能会等很久或失败，可多尝试几次。

    使用命令`ionic resources --splash` 或 `ionic resources --icon` 可单独生成图片或图标

    * ionic默认使用缓存的图片。如果想去掉缓存重新生成，可对图片稍作修改再重新生成。

- 3.不使用命令生成图片和图标的，可以将图片图标文件按照指定的格式放在resources文件夹下，然后在config.xml文件中配置。

```xml
    <platform name="android">
        <icon src="resources\android\icon\drawable-ldpi-icon.png" density="ldpi"/>
        <icon src="resources\android\icon\drawable-mdpi-icon.png" density="mdpi"/>
        <icon src="resources\android\icon\drawable-hdpi-icon.png" density="hdpi"/>
        <icon src="resources\android\icon\drawable-xhdpi-icon.png" density="xhdpi"/>
        <icon src="resources\android\icon\drawable-xxhdpi-icon.png" density="xxhdpi"/>
        <icon src="resources\android\icon\drawable-xxxhdpi-icon.png" density="xxxhdpi"/>
        <splash src="resources\android\splash\drawable-land-ldpi-screen.png" density="land-ldpi"/>
        <splash src="resources\android\splash\drawable-land-mdpi-screen.png" density="land-mdpi"/>
        <splash src="resources\android\splash\drawable-land-hdpi-screen.png" density="land-hdpi"/>
        <splash src="resources\android\splash\drawable-land-xhdpi-screen.png" density="land-xhdpi"/>
        <splash src="resources\android\splash\drawable-land-xxhdpi-screen.png" density="land-xxhdpi"/>
        <splash src="resources\android\splash\drawable-port-ldpi-screen.png" density="port-ldpi"/>
        <splash src="resources\android\splash\drawable-port-mdpi-screen.png" density="port-mdpi"/>
        <splash src="resources\android\splash\drawable-port-hdpi-screen.png" density="port-hdpi"/>
        <splash src="resources\android\splash\drawable-port-xhdpi-screen.png" density="port-xhdpi"/>
        <splash src="resources\android\splash\drawable-port-xxhdpi-screen.png" density="port-xxhdpi"/>
    </platform>
```