我们的示例仅要求用户进行身份验证，并且已针对应用程序中的每个URL进行了身份验证。我们可以通过向http.authorizeRequests（）方法添加多个子项来指定URL的自定义要求。 例如：

```
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()                                                                1
            .antMatchers("/resources/**", "/signup", "/about").permitAll()                  2
            .antMatchers("/admin/**").hasRole("ADMIN")                                      3
            .antMatchers("/db/**").access("hasRole('ADMIN') and hasRole('DBA')")            4
            .anyRequest().authenticated()                                                   5
            .and()
        // ...
        .formLogin();
}
```

1：http.authorizeRequests（）方法有多个子节点，每个匹配器按其声明的顺序进行考虑。

2：我们指定了任何用户都可以访问的多种URL模式。特别是，如果URL以“/ resources /”，“/ signup”或“/ about”开头，任何用户都可以访问请求。

3：任何以“/ admin /”开头的URL都将仅限于具有“ROLE\_ADMIN”角色的用户。您会注意到，由于我们正在调用hasRole方法，因此我们不需要指定“ROLE\_”前缀。

4：任何以“/ db /”开头的URL都要求用户同时拥有“ROLE\_ADMIN”和“ROLE\_DBA”。 您会注意到，由于我们使用的是hasRole表达式，因此我们不需要指定“ROLE\_”前缀。

5：任何尚未匹配的URL只需要对用户进行身份验证

