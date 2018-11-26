Spring Boot提供了一个spring-boot-starter-security启动程序，它将Spring Security相关的依赖项聚合在一起。利用starter最简单和首选的方法是使用IDE集成\([Eclipse](http://joshlong.com/jl/blogPost/tech_tip_geting_started_with_spring_boot.html)、[IntelliJ](https://www.jetbrains.com/help/idea/spring-boot.html#d1489567e2)、[NetBeans](https://github.com/AlexFalappa/nb-springboot/wiki/Quick-Tour)\)或通过[https://start.spring.io](https://start.spring.io)使用[Spring Initializr](https://docs.spring.io/initializr/docs/current/reference/htmlsingle/)。

或者，可以手动添加启动器

**pom.xml**

```
<dependencies>
    <!-- ... other dependency elements ... -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
</dependencies>
```

由于Spring Boot提供Maven BOM来管理依赖版本，因此无需指定版本。 如果您希望覆盖Spring Security版本，可以通过提供Maven属性来实现：

**pom.xml**

```
<properties>
    <!-- ... -->
    <spring-security.version>5.1.1.RELEASE</spring.security.version>
</dependencies>
```

由于Spring Security仅在主要版本中进行了重大更改，因此使用Spring Boot的较新版本的Spring Security是安全的。但是，有时可能还需要更新Spring Framework的版本。 这可以通过添加Maven属性轻松完成：

**pom.xml**

```
<properties>
    <!-- ... -->
    <spring.version>5.1.1.RELEASE</spring.version>
</dependencies>
```

如果您正在使用LDAP，OpenID等其他功能，则还需要包含相应的功能[Chapter 4,Project Modules](https://docs.spring.io/spring-security/site/docs/5.1.1.RELEASE/reference/htmlsingle/#modules)。

