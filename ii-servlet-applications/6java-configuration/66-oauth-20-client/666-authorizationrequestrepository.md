`AuthorizationRequestRepository`负责`OAuth2AuthorizationRequest`的持久性，从授权请求启动到收到授权响应（回调）。

> OAuth2AuthorizationRequest用于关联和验证授权响应。

AuthorizationRequestRepository的默认实现是HttpSessionOAuth2AuthorizationRequestRepository，它将OAuth2AuthorizationRequest存储在HttpSession中。

如果您想提供AuthorizationRequestRepository的自定义实现，该实现将OAuth2AuthorizationRequest的属性存储在Cookie中，您可以配置它，如以下示例所示：

```
@EnableWebSecurity
public class OAuth2ClientSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .oauth2Client()
                .authorizationCodeGrant()
                    .authorizationRequestRepository(this.cookieAuthorizationRequestRepository())
                    ...
    }

    private AuthorizationRequestRepository<OAuth2AuthorizationRequest> cookieAuthorizationRequestRepository() {
        return new HttpCookieOAuth2AuthorizationRequestRepository();
    }
}
```



