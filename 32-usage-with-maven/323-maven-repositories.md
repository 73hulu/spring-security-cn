所有GA版本（即以.RELEASE结尾的版本）都部署到Maven Central，因此不需要在您的pom中声明其他Maven存储库。

如果您使用的是SNAPSHOT版本，则需要确保定义了Spring Snapshot存储库，如下所示：

**pom.xml**

```
<repositories>
    <!-- ... possibly other repository elements ... -->
    <repository>
        <id>spring-snapshot</id>
        <name>Spring Snapshot Repository</name>
        <url>https://repo.spring.io/snapshot</url>
    </repository>
</repositories>
```

如果您使用里程碑或候选发布版本，则需要确保已定义Spring Milestone存储库，如下所示：

**pom.xml**

```
<repositories>
    <!-- ... possibly other repository elements ... -->
    <repository>
        <id>spring-milestone</id>
        <name>Spring Milestone Repository</name>
        <url>https://repo.spring.io/milestone</url>
    </repository>
</repositories>
```



