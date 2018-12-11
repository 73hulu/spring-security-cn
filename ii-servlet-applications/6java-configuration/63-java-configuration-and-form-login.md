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

使用JSP为我们当前配置实现的示例登录页面如下所示：

> 下面的登录页面代表我们当前的配置。如果某些默认设置不符合我们的需求，我们可以轻松更新配置。

```
<c:url value="/login" var="loginUrl"/>
<form action="${loginUrl}" method="post">       1
    <c:if test="${param.error != null}">        2
        <p>
            Invalid username and password.
        </p>
    </c:if>
    <c:if test="${param.logout != null}">       3
        <p>
            You have been logged out.
        </p>
    </c:if>
    <p>
        <label for="username">Username</label>
        <input type="text" id="username" name="username"/>  4
    </p>
    <p>
        <label for="password">Password</label>
        <input type="password" id="password" name="password"/>  5
    </p>
    <input type="hidden"                        6
        name="${_csrf.parameterName}"
        value="${_csrf.token}"/>
    <button type="submit" class="btn">Log in</button>
</form>
```

1：对/ login URL的POST将尝试对用户进行身份验证

2：如果存在查询参数错误，则尝试进行身份验证并失败

3：如果存在查询参数注销，则表示用户已成功注销

4：用户名必须作为名为username的HTTP参数出现

5：密码必须作为名为password的HTTP参数出现

6：我们必须在“包含CSRF令牌”一节中了解更多信息[the section called “Include the CSRF Token”](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#csrf-include-csrf-token)，请参阅第10.6节“跨站点请求伪造（CSRF）” [Section 10.6, “Cross Site Request Forgery \(CSRF\)”](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#csrf)部分的参考

