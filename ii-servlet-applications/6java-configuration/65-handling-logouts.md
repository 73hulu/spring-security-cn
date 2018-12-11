使用WebSecurityConfigurerAdapter时，会自动应用注销功能。默认情况下，访问 /logout  URL将通过以下方式注销用户：

* 使HTTP Session无效
* 清理已配置的任何RememberMe身份验证
* 清除SecurityContextHolder
* 重定向到 /login?logout

但是，与配置登录功能类似，您还可以使用各种选项来进一步自定义注销要求：

```
protected void configure(HttpSecurity http) throws Exception {
    http
        .logout()                                                                    1
            .logoutUrl("/my/logout")                                                 2
            .logoutSuccessUrl("/my/index")                                           3
            .logoutSuccessHandler(logoutSuccessHandler)                              4
            .invalidateHttpSession(true)                                             5
            .addLogoutHandler(logoutHandler)                                         6
            .deleteCookies(cookieNamesToClear)                                       7
            .and()
        ...
}
```

1：提供注销支持。 使用WebSecurityConfigurerAdapter时会自动应用此选项。

2：触发注销的URL（默认为/ logout）。如果启用了CSRF保护（默认），则该请求也必须是POST。有关更多信息，请参阅[JavaDoc ](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configurers/LogoutConfigurer.html#logoutUrl-java.lang.String-)

3：注销后重定向到的URL。默认是/login?logout。有关更多信息，请参阅[JavaDoc ](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configurers/LogoutConfigurer.html#logoutUrl-java.lang.String-)。

4：我们指定一个自定义的LogoutSuccessHandler。如果指定了此参数，则忽略logoutSuccessUrl（）。有关更多信息，请参阅[JavaDoc](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configurers/LogoutConfigurer.html#logoutSuccessHandler-org.springframework.security.web.authentication.logout.LogoutSuccessHandler-)。

5：指定在注销时是否使HttpSession无效。默认的是true。覆盖SecurityContextLogoutHandler配置

6：增加一个LogoutHandler。默认情况下，SecurityContextLogoutHandler被添加为最后一个LogoutHandler。

7：允许指定在注销成功时删除的cookie的名称。这是显式添加CookieClearingLogoutHandler的快捷方式。

> 当然，也可以使用XML名称空间表示法配置注销。有关更多详细信息，请参阅Spring Security XML Namespace部分中logout元素   [logout element](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#nsa-logout)的文档。

通常，为了自定义注销功能，您可以添加LogoutHandler或LogoutSuccessHandler实现。对于许多常见的场景，这些处理程序在使用fluent API时被隐藏起来应用。

