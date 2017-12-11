


- jtds Network error IOException Connection refused connect 的错误

    ```
    启动SQL2005的TCP/IP连接，因为默认的情况下是禁用TCP/IP的；
    打开 sql Server configuration manager，选择mssqlserver协议,然后右边窗口有个tcp/ip协议，然后启动它，重启sqlserver服务后试下看是否能解决问题
    ```