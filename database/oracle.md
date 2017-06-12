
- [创建表空间](#创建表空间)

# 创建表空间

- 查询datafile `select file_name from dba_data_files;`

- 创建表空间：

    ```
        create tablespace 表间名 datafile '数据文件名' size 表空间大小

        create tablespace NNDJ_CMS logging datafile 'E:\oracledb\oradata\orcl\nndj_cms.dbf' size 125m autoextend off;

        临时表空间：create temporary tablespace gx_fda_www_temp tempfile 'E:\oracledb\oradata\orcl\gx_fda_www_temp.dbf' size 125m autoextend off;
    ```

- 建好tablespace, 就可以建用户了

    ```
        create user 用户名 identified by 密码 default tablespace 表空间表;

        create user gx_fda_www identified by 123456 default tablespace gx_fda_www temporary tablespace gx_fda_www_temp;

    ```

    - 查看用户

    `select username,password from dba_users;`

    - 查看用户和默认表空间的关系

    `select username,default_tablespace from dba_users;`

    - 修改用户口令

    `格式 alter user 用户名 identified by 新密码;`

- 授权用户 若要创建跨用户的视图则要加入 select any table 的权限

    ```
        grant connect,resource,dba,select any table,drop any synonym to gx_fda_www;
    ```

- 加大空间

    ```
    alter tablespace gx_fda_mobile add datafile 'E:\oracledb\oradata\orcl\gx_fda_mobile.dbf' size 1024m;
    ```

- 删除表空间

    ```
    DROP TABLESPACE gx_fda_app INCLUDING CONTENTS AND DATAFILES;
    ```

- 删除用户
    ```
    drop user gx_fda_app cascade;
    ```

- 查看剩余空间
    ```
    select sum(bytes/1024/1024) sizeMB from dba_free_space z where z.tablespace_name='GX_FDA_OA';

    select file_name,tablespace_name,bytes/1024/1024 from dba_data_files where tablespace_name='GX_FDA_OA';
    ```
- 加大数据文件
    ```
    alter database datafile 'E:\ORACLEDB\ORADATA\ORCL\GX_FDA_OA.DBF' resize 5120M;
    ```

# 导入导出数据

1.使用数据库连接工具查询数据库文件路径

	--查询数据库文件
	select * from dba_directories;

2.登录linux服务器

	Linux 连接数据库
	su - oracle

	----例子---
	--正式
	/home/oracle/app/oracle/admin/orcl/dpdump/
	--测试
	/opt/oracle/admin/FDATEST/dpdump/
	--本地
	E:\oracledb/admin/orcl/dpdump/
	---------

3.导出

- expdp

	在linux命令中输入
	expdp 用户名/密码 directory=DATA_PUMP_DIR dumpfile=文件名.dump schemas=表空间
	如
	expdp NNDJ_CMS/123456 directory=DATA_PUMP_DIR dumpfile=GGFDA2017060901.dump schemas=NNDJ_CMS

- exp

    exp userid=NNDJ_CMS/123456 file=/home/oracle/app/oracle/admin/orcl/dpdump/NNDJ_CMS2017061202.dmp owner=NNDJ_CMS

4.导入

- impdp
	登录目标服务器
	把dump文件拷到数据库文件路径下
	输入：
	su - oracle
	impdp 用户名/密码 directory=DATA_PUMP_DIR dumpfile=文件名.dump table_exists_action=replace schemas=表空间
	如
	impdp LZ_FDA_DATACENTER/123456 directory=DATA_PUMP_DIR dumpfile=LZ_FDA_DATACENTER2017060301.dump table_exists_action=replace schemas=LZ_FDA_DATACENTER,LZFDA_DC_EXCHANGE,LZ_FDA_AIPCASE,LZ_FDA_CMS,LZ_FDA_REPORT,LZ_FDA_SAFE,LZ_FDA_SUPEXA,LZ_FDA_SYS

- imp
	imp userid=NNDJ_CMS/123456 file=E:\oracledb\admin\orcl\dpdump\NNDJ_CMS2017061202.dmp fromuser=NNDJ_CMS touser=NNDJ_CMS