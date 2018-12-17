OAuth 2.0客户机特性提供了对OAuth 2.0授权框架[OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749#section-1.1)中定义的客户机角色的支持。

主要特点如下：

* [Authorization Code Grant](https://tools.ietf.org/html/rfc6749#section-1.3.1)
* [Client Credentials Grant](https://tools.ietf.org/html/rfc6749#section-1.3.4)
* Servlet环境的WebClient扩展[extension for Servlet Environments](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#servlet-webclient)（用于创建受保护的资源请求）

HttpSecurity.oauth2Client\(\)提供了许多用于自定义OAuth 2.0 Client的配置选项。以下代码显示了oauth2Client（）DSL可用的完整配置选项：

```
@EnableWebSecurity
public class OAuth2ClientSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .oauth2Client()
                .clientRegistrationRepository(this.clientRegistrationRepository())
                .authorizedClientRepository(this.authorizedClientRepository())
                .authorizedClientService(this.authorizedClientService())
                .authorizationCodeGrant()
                    .authorizationRequestRepository(this.authorizationRequestRepository())
                    .authorizationRequestResolver(this.authorizationRequestResolver())
                    .accessTokenResponseClient(this.accessTokenResponseClient());
    }
}
```



