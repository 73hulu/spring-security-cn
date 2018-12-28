OAuth2AccessTokenResponseClient的主要角色是在授权服务器的令牌端点将授权许可凭据交换为访问令牌凭据。

对于authorization\_code授权，OAuth2AccessTokenResponseClient的默认实现是`DefaultAuthorizationCodeTokenResponseClient`，它使用RestOperations在令牌端点将授权代码交换为访问令牌。

DefaultAuthorizationCodeTokenResponseClient非常灵活，因为它允许您自定义令牌请求的预处理或令牌响应的后处理。

如果需要定制令牌请求的预处理，可以为DefaultAuthorizationCodeTokenResponseClient.setRequestEntityConverter\(\)提供一个自定义的转换器Converter&lt;OAuth2AuthorizationCodeGrantRequest, RequestEntity&lt;?&gt;&gt;。默认实现OAuth2AuthorizationCodeGrantRequestEntityConverter构建标准OAuth 2.0访问令牌请求的RequestEntity表示。但是，提供自定义转换器将允许您扩展标准令牌请求并添加自定义参数。

> Important
>
> 自定义转换器必须返回OAuth 2.0访问令牌请求的有效RequestEntity表示，该表示由预期的OAuth 2.0提供程序理解。

另一方面，如果您需要自定义令牌响应的后处理，则需要使用自定义配置的RestOperations提供DefaultAuthorizationCodeTokenResponseClient.setRestOperations（）。 默认的RestOperations配置如下：

```
RestTemplate restTemplate = new RestTemplate(Arrays.asList(
        new FormHttpMessageConverter(),
        new OAuth2AccessTokenResponseHttpMessageConverter()));

restTemplate.setErrorHandler(new OAuth2ErrorResponseErrorHandler());
```

> 当发送OAuth 2.0访问令牌请求时，需要使用Spring MVC FormHttpMessageConverter。

OAuth2AccessTokenResponseHttpMessageConverter是OAuth 2.0访问令牌响应的HttpMessageConverter。您可以使用自定义Converter &lt;Map &lt;String，String&gt;，OAuth2AccessTokenResponse&gt;提供OAuth2AccessTokenResponseHttpMessageConverter.setTokenResponseConverter（），该选项用于将OAuth 2.0访问令牌响应参数转换为OAuth2AccessTokenResponse。

OAuth2ErrorResponseErrorHandler是一个ResponseErrorHandler，可以处理OAuth 2.0错误（400 Bad Request）。它使用OAuth2ErrorHttpMessageConverter将OAuth 2.0 Error参数转换为OAuth2Error。

无论您是自定义DefaultAuthorizationCodeTokenResponseClient还是提供自己的OAuth2AccessTokenResponseClient实现，您都需要对其进行配置，如以下示例所示：

```
@EnableWebSecurity
public class OAuth2ClientSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .oauth2Client()
                .authorizationCodeGrant()
                    .accessTokenResponseClient(this.customAccessTokenResponseClient())
                    ...
    }

    private OAuth2AccessTokenResponseClient<OAuth2AuthorizationCodeGrantRequest> customAccessTokenResponseClient() {
        ...
    }
}
```



