# cordova 热更新

- 参考hcp/【Ionic】Ionic实现iOS与Android端代码『热更新』与Android升级下载功能 （ v1.3.x版本 ）.html

1. 安装 cordova-hot-code-push-cli

    ```
        npm install -g cordova-hot-code-push-cli
    ```

2. 在项目中添加插件

    ```
        cordova plugin add cordova-hot-code-push-plugin
    ```

    本地调试(可不安装)：
    ```
        cordova plugin add cordova-hot-code-push-local-dev-addon
    ```

    !!发布app时要移除这个插件
    ```
        cordova plugin rm cordova-hot-code-push-local-dev-addon
    ```

3. 初始化配置模板

    ```
        cordova-hcp init
    ```

    - content_url 服务器上www文件夹的路径，如<http://xxxx/xxx/apphcp/www/> ，服务器上 部署项目路径+apphcp/www/下放着原www目录下的所有文件。

    - 初始化后会生成cordova-hcp.json文件，之后每次更新都会以这个为模板生成chcp.json文件.

      * content_url

      服务端URL, 也就是你所有web内容文件的位置. 插件会把它作为下载新的清单文件、新的web内容文件的 base url. 此项必须.

      * release

      任何字符串. 每次release应该唯一. 插件基于这个才知道有没有新版本release. 此项必须.

      重要: 插件只比较release字符串是否相等, 如果不等，就认为服务端有新版本.（!!!不会比较大小!!!）



4. 生成chcp.json和chcp.manifest文件

    ```
        cordova-hcp build
    ```

5. 在config.xml文件中加入

    ```
        <chcp>
            <!--内核版本-->
            <native-interface version="1" />
            <config-file url="http://113.16.135.154:58088/gxfda_aipcase/apphcp/www/chcp.json" />
        </chcp>
    ```

    - 注意要具体到chcp.json的路径

6. 实现热更新

    每次修改www目录下的文件后，执行`cordova-hcp build`，会更新chcp.json和chcp.manifest文件，然后将 www下的文件拷贝至服务器中的指定更新路径（即chcp.json中 content_url 指向的路径），可实现热更新。




