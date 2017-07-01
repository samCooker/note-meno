
* [as打jar和aar包](#as打jar和aar包)


# as打jar和aar包

- jar包与aar包的区别

    - jar是java字节码文件（class文件）的归档文件，其不包含android中的资源文件等信息；

    - aar是android中特有的归档文件，既包含字节码文件也包含android的资源文件等；

- 使用as打包后直接在对应module下生成jar和aar包

    - jar路径：moduleName/intermediates/bundles

    - aar路径：moduleName/outputs/aar