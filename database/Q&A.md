* [the password has expired](#the password has expired)

# the password has expired

1. 连接SQLplus

    `su - oracle`

    `sqlplus connect as sysdba`

- 查询密码的有效期设置，LIMIT字段是密码有效天数，默认180天。

    `SELECT * FROM dba_profiles WHERE profile='DEFAULT' AND resource_name='PASSWORD_LIFE_TIME';`

- 去掉密码的有效期设置

    `ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;`

- 修改密码

    `ALTER USER 用户名 IDENTIFIED BY 密码;`

    `ALTER USER MSXOA IDENTIFIED BY msx1234;`

- 如果账号被锁住，则需要解锁命令

  `alter user GX_FDA_MOBILE identified by oracle account unlock;`

# 无法删除用户

  ```
  SQL> select username,sid,serial# from v$session;
  USERNAME                              SID    SERIAL#
  ------------------------------ ---------- ----------
                                          1          1
                                          2          1
                                          3          1
                                          4          1
                                          5          1
                                          6          1
                                          7          1
  SYS                                     8          3
  A                                       9          4
  已选择9行。
  SQL> alter system kill session'9,4';
  系统已更改。
  SQL> drop user a cascade;//删除用户以及用户表空间下所有对象
  用户已丢弃。
  ```