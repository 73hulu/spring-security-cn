第一步是创建Spring Security Java Configuration。该配置创建一个名为`springSecurityFilterChain`的Servlet过滤器，它负责应用程序中的所有安全性（保护应用程序URL，验证提交的用户名和密码，重定向到登录表单等）。您可以在下面找到Spring Security Java Configuration的最基本示例：

```
import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.context.annotation.*;
import org.springframework.security.config.annotation.authentication.builders.*;
import org.springframework.security.config.annotation.web.configuration.*;

@EnableWebSecurity
public class WebSecurityConfig implements WebMvcConfigurer {

    @Bean
    public UserDetailsService userDetailsService() throws Exception {
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(User.withDefaultPasswordEncoder().username("user").password("password").roles("USER").build());
        return manager;
    }
}
```

这种配置确实没什么用，但它做了很多。 您可以在下面找到以下功能的摘要：

* 要求对应用程序中的每个URL进行身份验证
* 为您生成一个登录表单
* 允许具有Username用户和Password密码的用户使用基于表单的身份验证进行身份验证
* 允许用户注销
* CSRF攻击（[CSRF attack](https://en.wikipedia.org/wiki/Cross-site_request_forgery)）预防
* 会话固定（[Session Fixation](https://en.wikipedia.org/wiki/Session_fixation)）保护
* 安全标头集成
  * HTTP为安全请求提供了严格的传输安全性（[HTTP Strict Transport Security](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)）
  * [X-Content-Type-Options](https://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx)集成
  * 缓存控制（稍后可由应用程序覆盖以允许缓存静态资源）
  * [X-XSS-Protection](https://msdn.microsoft.com/en-us/library/dd565647%28v=vs.85%29.aspx)集成

  * X-Frame-Options集成，帮助防止点击劫持[Clickjacking](https://en.wikipedia.org/wiki/Clickjacking)
* 




