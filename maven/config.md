# 指定JDK编译

在 <plugins>标签下加入

```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.1</version>
    <configuration>
        <!--  JDK版本 -->
        <source>1.7</source>
        <!--  JDK版本 -->
        <target>1.7</target>
        <encoding>UTF-8</encoding>
    </configuration>
</plugin>
```