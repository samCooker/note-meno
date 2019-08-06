
- [启动oracle](#启动oracle)
- [创建表空间](#创建表空间)
- [导入导出数据](#导入导出数据)

# 启动oracle

- linux

    1. 登陆服务器，切换到oracle用户`su - oracle`

    2. 查看监听状态 `lsnrctl status`, 启动监听 `lsnrctl start`

    3. 以system用户身份登陆oracle  `sqlplus conn as sysdba`

    4. 启动命令 `startup`

# 创建表空间

- 查询datafile `select file_name from dba_data_files;`

- 创建表空间：

    ```
        create tablespace 表间名 datafile '数据文件名' size 表空间大小
        临时表空间：
        create temporary tablespace 临时表空间名 tempfile 文件路径 size 大小 autoextend off;
        列：
        create tablespace GX_FDA_SYS logging datafile '/home/oracle/app/oradata/shicx/GX_FDA_SYS.dbf' size 512m autoextend off;
        create temporary tablespace GX_FDA_SYS_TEMP tempfile '/home/oracle/app/oradata/shicx/GX_FDA_SYS_TEMP.dbf' size 125m autoextend off;

        create tablespace GX_FDA_OA logging datafile '/home/oracle/app/oradata/shicx/GX_FDA_OA.dbf' size 512m autoextend off;
        create temporary tablespace GX_FDA_OA_TEMP tempfile '/home/oracle/app/oradata/shicx/GX_FDA_OA_TEMP.dbf' size 125m autoextend off;
    ```

- 建好tablespace, 就可以建用户了

    ```
        create user 用户名 identified by 密码 default tablespace 表空间表;

        create user MSXOA identified by 123456 default tablespace GX_FDA_SYS;
        create user GX_FDA_OA identified by gxfda1234 default tablespace GX_FDA_OA temporary tablespace GX_FDA_OA_TEMP;

    ```

    - 查看用户

    `select username,password from dba_users;`

    - 查看用户和默认表空间的关系

    `select username,default_tablespace from dba_users;`

    - 修改用户口令

    `格式 alter user 用户名 identified by 新密码;`

- 授权用户 若要创建跨用户的视图则要加入 select any table 的权限

    ```
        grant connect,resource,dba,select any table,drop any synonym to lz_fda_aipcase;
        grant connect,resource to MSXOA;
    ```

- 加大空间

    ```
    alter tablespace NNGOV_OA add datafile 'E:\oracledb\oradata\orcl\NNGOV_OA.dbf' size 7024m;
    ```

- 删除表空间

    ```
    DROP TABLESPACE GX_FDA_OA INCLUDING CONTENTS AND DATAFILES;
    DROP TABLESPACE GX_FDA_SYS INCLUDING CONTENTS AND DATAFILES;
    ```

- 删除用户
    ```
    drop user gx_fda_oa cascade;
    drop user gx_fda_sys cascade;
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

- 修改默认表空间
    ```
    alter user user_name default tablespace tbs_name;
    alter user lz_fda_aipcase default tablespace lz_fda_aipcase;
    设置数据库的默认临时表空间:
    Alter database default temporary tablespace temp_tbs_name;
    ```

create tablespace GGFDA_MRCD logging datafile 'E:\oracledb\oradata\orcl\GGFDA_MRCD.dbf' size 125m autoextend off;
create temporary tablespace GGFDA_MRCD_TEMP tempfile 'E:\oracledb\oradata\orcl\GGFDA_MRCD_TEMP.dbf' size 125m autoextend off;
create user GGFDA_MRCD identified by 123456 default tablespace GGFDA_MRCD temporary tablespace GGFDA_MRCD_TEMP;
grant connect,resource,dba,select any table,drop any synonym to GX_FDA_OA;

# 导入导出数据

1.使用数据库连接工具查询数据库文件路径

	--查询数据库文件
	select * from dba_directories;

2.登录linux服务器

	Linux 连接数据库
	su - oracle

	----例子---
	--
	/home/oracle/app/oracle/admin/orcl/dpdump/
	--
	/opt/oracle/admin/FDATEST/dpdump/
	--
	E:\oracledb/admin/orcl/dpdump/
	---------

3.导出

- expdp

	在linux命令中输入
	expdp 用户名/密码 directory=DATA_PUMP_DIR dumpfile=文件名.dump schemas=表空间
	如
	expdp GX_FDA_OA/123456 directory=DATA_PUMP_DIR dumpfile=GX_FDA_OA20180728.DUMP schemas=GX_FDA_OA
	expdp ggfda_mrcd/123456@orclpdb directory=DATA_PUMP_DIR dumpfile=ggfda_mrcd2017072301.dump schemas=ggfda_mrcd
	
	expdp GX_FDA_MOBILE/nhy6mju7123 directory=DATA_PUMP_DIR dumpfile=gxfda_mobile_2019062001.dump tables=SYS_USER,SYS_USER_ORG_MAPPING

    * 12c 导出 11g ，加入版本号 version=11.2.0.1.0 （版本号查看`select version from v$instance;`）

    expdp ggfda_mrcd/123456@orclpdb directory=DATA_PUMP_DIR dumpfile=ggfda_mrcd2017072301_11g.dump schemas=ggfda_mrcd version=11.2.0.1.0

- exp

    exp userid=ggfda_mrcd/123456 file=/home/oracle/app/oracle/admin/orcl/dpdump/ggfda_mrcd2017061202.dmp owner=ggfda_mrcd

4.导入

- impdp

	登录目标服务器
	把dump文件拷到数据库文件路径下
	输入：
	su - oracle
	impdp 用户名/密码 directory=DATA_PUMP_DIR dumpfile=文件名.dump table_exists_action=replace schemas=表空间
	如
	impdp GX_FDA_OA/gxfda1234 directory=DATA_PUMP_DIR dumpfile=gx_fda_oa2018072401.dump table_exists_action=replace schemas=GX_FDA_OA

	impdp ggfda_mrcd/123456 directory=DATA_PUMP_DIR dumpfile=ggfda_mrcd2017072301_11g.dump table_exists_action=replace schemas=ggfda_mrcd
	
	impdp GX_FDA_MOBILE/123456 directory=DATA_PUMP_DIR dumpfile=gxfda_mobile_2019062001.dump table_exists_action=replace tables=SYS_USER,SYS_USER_ORG_MAPPING

    表空间不同

    impdp system/FSYoracle123456 directory=DATA_PUMP_DIR dumpfile=MSX_OA20180724.DUMP table_exists_action=replace remap_schema=MSX_OA:MSXOA

    DATA_OPTIONS=SKIP_CONSTRAINT_ERRORS

- imp

	imp userid=NNDJ_CMS/123456 file=E:\oracledb\admin\orcl\dpdump\NNDJ_CMS2017061202.dmp fromuser=NNDJ_CMS touser=NNDJ_CMS