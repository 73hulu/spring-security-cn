在没有Spring Boot的情况下使用Spring Security时，首选方法是利用Spring Security的BOM来确保在整个项目中使用一致的Spring Security版本。

**pom.xml**

```
<dependencyManagement>
    <dependencies>
        <!-- ... other dependency elements ... -->
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-bom</artifactId>
            <version>5.1.1.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

最小的Spring Security Maven依赖项通常如下所示：

**pom.xml**

```
<dependencies>
    <!-- ... other dependency elements ... -->
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-config</artifactId>
    </dependency>
</dependencies>
```

如果您正在使用LDAP，OpenID等其他功能，则还需要包含相应的功能[Chapter 4,Project Modules](https://docs.spring.io/spring-security/site/docs/5.1.1.RELEASE/reference/htmlsingle/#modules)。

Spring Security针对Spring Framework 5.1.1.RELEASE构建，但通常应该适用于任何较新版本的Spring Framework 5.x许多用户将遇到的问题是Spring Security的传递依赖性解决了Spring Framework 5.1.1.RELEASE，这可能会导致 奇怪的类路径问题。解决此问题的最简单方法是在pom.xml的&lt;dependencyManagement&gt;部分中使用spring-framework-bom，如下所示：

**pom.xml**

```
<dependencyManagement>
    <dependencies>
        <!-- ... other dependency elements ... -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>5.1.1.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

这将确保Spring Security的所有传递依赖项都使用Spring 5.1.1.RELEASE模块。

> 这种方法使用Maven的“物料清单”（BOM）概念，仅适用于Maven 2.0.9+。有关如何解析依赖关系的其他详细信息，请参阅[Maven’s Introduction to the Dependency Mechanism documentation](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)。



