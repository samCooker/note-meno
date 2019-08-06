
# linux(mac) 问题

* mysql command not found

 1. 打开终端,输入： `cd ~` 会进入~文件夹

 2. 然后输入：`sudo vim .bash_profile`,回车执行，需要输入root用户密码。sudo是使用root用户修改环境变量文件。

 3. 在文档的最下方输入：`export PATH=${PATH}:/usr/local/mysql/bin`,然后esc退出insert状态，并在最下方输入:wq保存退出。

 4. 输入：`source .bash_profile`,回车执行，运行环境变量。

* Mysql5.7.10修改root初始密码

- linux

 1. 编辑 /etc/my.cnf的mysql配置文件

 2. 加入 `skip-grant-tables`

 3. 重启

- mac

1.
点击系统偏好设置->最下边点MySQL，在弹出页面中，关闭服务
2.
进入终端输入：cd /usr/local/mysql/bin/
回车后 登录管理员权限 sudo su
回车后输入以下命令来禁止mysql验证功能 ./mysqld_safe --skip-grant-tables &
回车后mysql会自动重启（偏好设置中mysql的状态会变成running）
3.
输入命令 ./mysql
回车后，输入命令 FLUSH PRIVILEGES;
回车后，输入命令 SET PASSWORD FOR 'root'@'localhost' = PASSWORD('你的新密码');

SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');

# 创建用户

CREATE USER 'shicx'@'%' IDENTIFIED BY "123";

drop user 'shicx'@'%';

grant all privileges on *.* to root@'%' identified by 'FSY8ik,9ol.';


# Mysql 修改密码加密方式

修改密码加密方式，改成mysql_native_password

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';

然后修改密码：

SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword');
或者执行命令flush privileges使权限配置项立即生效。