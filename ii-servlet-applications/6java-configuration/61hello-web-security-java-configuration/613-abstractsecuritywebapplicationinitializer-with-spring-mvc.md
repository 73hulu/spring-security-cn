如果我们在应用程序的其他地方使用Spring，我们可能已经有了一个加载Spring配置的WebApplicationInitializer。如果我们使用以前的配置，我们会收到错误。相反，我们应该使用现有的ApplicationContext注册Spring Security。例如，如果我们使用Spring MVC，我们的SecurityWebApplicationInitializer将如下所示：

```
import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
    extends AbstractSecurityWebApplicationInitializer {

}
```

这只会为应用程序中的每个URL注册springSecurityFilterChain过滤器。之后，我们将确保在现有的ApplicationInitializer中加载WebSecurityConfig。例如，如果我们使用Spring MVC，它将被添加到getRootConfigClasses（）中

```
public class MvcWebApplicationInitializer extends
        AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[] { WebSecurityConfig.class };
    }

    // ... other overrides ...
}
```



