通常，LogoutHandler实现类表示能够参与注销处理的类。预计将调用它们以进行必要的清理。因此，他们不应该抛出异常。 提供了各种实现：

* [PersistentTokenBasedRememberMeServices](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/rememberme/PersistentTokenBasedRememberMeServices.html)

* [TokenBasedRememberMeServices](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/rememberme/TokenBasedRememberMeServices.html)

* [CookieClearingLogoutHandler](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/logout/CookieClearingLogoutHandler.html)
* [CsrfLogoutHandler](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/csrf/CsrfLogoutHandler.html)
* [SecurityContextLogoutHandler](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/web/authentication/logout/SecurityContextLogoutHandler.html)

更多详细信息请查阅[Section 10.5.4, “Remember-Me Interfaces and Implementations”](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#remember-me-impls)

而不是直接提供LogoutHandler实现，fluent API还提供了快捷方式，提供了相应的LogoutHandler实现。比如，deleteCookies（）允许指定在注销成功时删除的一个或多个cookie的名称。与添加CookieClearingLogoutHandler相比，这是一种快捷方式。

