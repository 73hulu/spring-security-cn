到目前为止，我们的WebSecurityConfig仅包含有关如何验证用户身份的信息。Spring Security如何知道我们要求所有用户进行身份验证？Spring Security如何知道我们想要支持基于表单的身份验证？原因是WebSecurityConfigurerAdapter在configure（HttpSecurity http）方法中提供了一个默认配置，如下所示：

```
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
            .anyRequest().authenticated()
            .and()
        .formLogin()
            .and()
        .httpBasic();
}
```

上面的默认配置：

* 确保对我们的应用程序的任何请求都要求用户进行身份验证
* 允许用户使用基于表单的登录进行身份验证
* 允许用户使用HTTP基本身份验证进行身份验证 

您会注意到此配置与XML命名空间配置非常相似：

```
<http>
    <intercept-url pattern="/**" access="authenticated"/>
    <form-login />
    <http-basic />
</http>
```

与关闭XML标记等价的Java配置是使用and\(\)方法表示的，该方法允许我们继续配置父标记。如果你读了代码，它也是有意义的。我想配置授权请求并配置表单登录并配置HTTP基本身份验证。



