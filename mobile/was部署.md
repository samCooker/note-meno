- https://172.18.0.3:9043/ibm/console/logon.jsp

admin
cde3vfr4

如果知道服务的端口，发布之前最好在那台机器用这个命令查一下

`netstat -nap | grep 9080`

停服务后，用ps -ef | grep java查看是否停完

查看was进程

`ps -ef | grep was`

1. 停止服务 ![图片](/mobile/res/was-1.png '')

2. 检查是否已经停止 `ps -ef | grep was`

3. 启动服务 ![图片](/mobile/res/was-2.png '')