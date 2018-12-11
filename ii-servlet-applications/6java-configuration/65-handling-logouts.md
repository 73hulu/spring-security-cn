使用WebSecurityConfigurerAdapter时，会自动应用注销功能。默认情况下，访问 /logout  URL将通过以下方式注销用户：

* 使HTTP Session无效
* 清理已配置的任何RememberMe身份验证
* 清除SecurityContextHolder
* 重定向到 /login?logout

但是，与配置登录功能类似，您还可以使用各种选项来进一步自定义注销要求：

```
protected void configure(HttpSecurity http) throws Exception {
    http
        .logout()                                                                1
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



