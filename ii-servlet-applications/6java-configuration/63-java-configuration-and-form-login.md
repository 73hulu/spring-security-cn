当您被提示登录时，您可能想知道登录表单的来源，因为我们没有提及任何HTML文件或JSP。由于Spring Security的默认配置不显式地设置登录页面的URL，因此Spring Security会根据启用的功能自动生成一个URL，和使用标准流程提交登录URL的值，在登录之后将向默认的目标URL发送用户信息等。

虽然自动生成的登录页面便于快速启动和运行，但大多数应用程序都希望提供自己的登录页面。 为此，我们可以更新我们的配置，如下所示：

```
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
            .anyRequest().authenticated()
            .and()
        .formLogin()
            .loginPage("/login")   1
            .permitAll();          2
}
```

> 1：更新的配置指定登录页面的位置。
>
> 2：我们必须授予所有用户（即未经身份验证的用户）访问我们的登录页面的权限。formLogin\(\).permitAll\(\)方法允许为基于表单的登录相关联的所有url授予所有用户访问权。



