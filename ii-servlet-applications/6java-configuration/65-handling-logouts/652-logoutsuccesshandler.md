在LogoutFilter成功注销后调用LogoutSuccessHandler，以处理例如 重定向或转发到适当的目的地。注意，接口几乎与LogoutHandler相同，但可能会引发异常。

提供以下实现：

* [SimpleUrlLogoutSuccessHandler](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/logout/SimpleUrlLogoutSuccessHandler.html)

* HttpStatusReturningLogoutSuccessHandler

如上所述，您不需要直接指定SimpleUrlLogoutSuccessHandler。相反，fluent API通过设置logoutSuccessUrl（）来提供快捷方式。这将在后面设置SimpleUrlLogoutSuccessHandler。发生注销后，将重定向到提供的URL。默认的是/login?logout。

HttpStatusReturningLogoutSuccessHandler在REST API类型场景中可能很有趣。与成功注销后重定向到URL不同，此logoutsuccessesshandler允许您提供返回的纯HTTP状态代码。如果未配置，则默认返回状态代码200。

