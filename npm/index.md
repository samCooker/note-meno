
# update

- npm install npm@latest -g

- update node

  * `sudo npm cacheclean -f`

  * `sudo npm install -g n`

  * `sudo n stable` or `sudo n x.x.x(version)`


# npm 代理

- 安装 `npm install -g cnpm --registry=https://registry.npm.taobao.org` ，使用cnpm (gzip 压缩支持) 命令行工具代替默认的 npm

# 使用国内镜像

镜像使用方法（三种办法任意一种都能解决问题，建议使用第三种，将配置写死，下次用的时候配置还在）:

1.通过config命令

npm config set registry https://registry.npm.taobao.org
npm info underscore （如果上面配置正确这个命令会有字符串response）
2.命令行指定

npm --registry https://registry.npm.taobao.org info underscore
3.编辑 ~/.npmrc 加入下面内容

registry = https://registry.npm.taobao.org

# 常见错误

- VCBuild不存在的错误

   ```
        MSBUILD : error MSB3428: 未能加载 Visual C++ 组件“VCBuild.exe”。要解决此问题，1) 安装 .NET Framework 2.0 SDK；2) 安装 Microsoft Visual Stu
       dio 2005；或 3) 如果将该组件安装到了其他位置，请将其位置添加到系统路径中。 [C:\Users\zongren\zongren.gitlab.io\node_modules\microtime\build\binding.sl
       n]
   ```

   使用npm安装windows build tools `npm install --global --production windows-build-tools`


