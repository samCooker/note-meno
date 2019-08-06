
1. docker安装

2. 安装依赖包

第一次安装时最后能够保证连网，如不能连网需要提前准备好相应的包。

保证虚拟机ok，docker已经安装好，同时将oracle包拷贝至centos6.6的容器中的 /oracle_package目录下。


   1. 开始安装

- 安装oracle所需要的 gcc* 、glibc*相关的包 

    gcc*在装的时候看到有很多个，每个都不是很大，只要网速不是特别差还是很快的。
    
    ```
    yum -y install gcc*
    yum -y install glibc*
    ```
    
    也可以指安装所需的包，并且要注意顺序：
    
    Oracle 对GCC的顺序：
    
    glibc-common-2.12-1.80.el6.x86_64.rpm
    kernel-headers-2.6.32-279.el6.x86_64.rpm
    libgcc-4.4.6-4.el6.x86_64.rpm
    glibc-2.12-1.80.el6.x86_64.rpm
    libgomp-4.4.6-4.el6.x86_64.rpm
    nscd-2.12-1.80.el6.x86_64.rpm
    glibc-headers-2.12-1.80.el6.x86_64.rpm
    glibc-devel-2.12-1.80.el6.x86_64.rpm
    mpfr-2.4.1-6.el6.x86_64.rpm
    ppl-0.10.2-11.el6.x86_64.rpm
    cloog-ppl-0.15.7-1.2.el6.x86_64.rpm
    cpp-4.4.6-4.el6.x86_64.rpm
    gcc-4.4.6-4.el6.x86_64.rpm
    注：以上是安装gcc，软件安装顺序不能错
    libstdc++-4.4.6-4.el6.x86_64.rpm
    libstdc++-devel-4.4.6-4.el6.x86_64.rpm
    gcc-c++-4.4.6-4.el6.x86_64.rpm
    注：以上是安装gcc-c++
    
    也可以使用yum的方式进行安装
    
    yum -y install gcc
    yum -y install make
    yum -y install binutils
    yum -y install gcc-c++
    yum -y install compat-libstdc++-33
    yum -y install elfutils-libelf-devel
    yum -y install elfutils-libelf-devel-static
    yum -y install ksh
    yum -y install libaio
    yum -y install libaio-devel
    yum -y install numactl-devel
    yum -y install sysstat
    yum -y install unixODBC
    yum -y install unixODBC-devel
    yum -y install pcre-devel