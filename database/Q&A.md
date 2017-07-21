* [the password has expired](#the password has expired)

# the password has expired

1. 连接SQLplus

    `sqlplus connect as sysdba`

- 查询密码的有效期设置，LIMIT字段是密码有效天数，默认180天。

    `SELECT * FROM dba_profiles WHERE profile='DEFAULT' AND resource_name='PASSWORD_LIFE_TIME';`

- 去掉密码的有效期设置

    `ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;`

- 修改密码

    `ALTER USER 用户名 IDENTIFIED BY 密码;`

- 如果账号被锁住，则需要解锁命令

  `alter user gx_fda_oa identified by oracle account unlock;`