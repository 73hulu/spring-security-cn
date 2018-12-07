如果您不使用Spring或Spring MVC，则需要将WebSecurityConfig传递到超类中以确保获取配置。你可以在下面找到一个例子:

```
import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
    extends AbstractSecurityWebApplicationInitializer {

    public SecurityWebApplicationInitializer() {
        super(WebSecurityConfig.class);
    }
}
```

SecurityWebApplicationInitializer将执行以下操作:

* 为应用程序中的每个URL自动注册springSecurityFilterChain过滤器
* 添加一个ContextLoaderListener来加载WebSecurityConfig。



