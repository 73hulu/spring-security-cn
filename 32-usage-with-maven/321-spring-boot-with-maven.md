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



