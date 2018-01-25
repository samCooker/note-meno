- 内存大小设置

  WINDOWS操作系统，修改catalina.bat文件；

  否则修改catalina.sh文件。只需要在文件的头部加上

  `set JAVA_OPTS="-Xms256m –Xmx512m -XX:PermSize=128m -XX:MaxPermSize=512m"`

  参数说明：

  -Xms：初始Heap大小，使用的最小内存,cpu性能高时此值应设的大一些

  -Xmx：java heap最大值，使用的最大内存

  上面两个值是分配JVM的最小和最大内存，取决于硬件物理内存的大小，建议均设为物理内存的一半。

  -XX:PermSize:设定内存的永久保存区域

  -XX:MaxPermSize:设定最大内存的永久保存区域