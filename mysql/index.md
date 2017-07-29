# mysql开放3306端口
- 修改mysql

1. 登陆mysql

   `mysql -u root -p`

2. 修改mysql库的user表，将host项，从localhost改为%。%这里表示的是允许任意host访问，如果只允许某一个ip访问，则可改为相应的ip，比如可以将localhost改为192.168.1.123，这表示只允许局域网的192.168.1.123这个ip远程访问mysql。

`
use mysql;
update user set host = '%' where user = 'root';
select host, user from user;
flush privileges;
`
- 防火墙开放3306端口

1. 打开防火墙配置文件
`
vi /etc/sysconfig/iptables
`

2. 增加下面一行
`
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
`
3. 重启防火墙
`
service  iptables restart
`

```
# Firewall configuration written by system-config-firewall
# Manual customization of this file is not recommended.
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -i eth0 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
-A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
-A FORWARD -p icmp -j ACCEPT
-A FORWARD -i lo -j ACCEPT
-A FORWARD -i eth0 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```