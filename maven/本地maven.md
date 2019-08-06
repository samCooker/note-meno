
# 制作本地安装包

  xxxx.jar 放到目录下

  执行命令：cmd 定位到目录下下

  mvn install:install-file -DgroupId=xxxx -DartifactId=xxxx -Dversion=xxx -Dpackaging=jar -Dfile=fileName.jar