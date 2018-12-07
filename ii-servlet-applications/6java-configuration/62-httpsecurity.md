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



