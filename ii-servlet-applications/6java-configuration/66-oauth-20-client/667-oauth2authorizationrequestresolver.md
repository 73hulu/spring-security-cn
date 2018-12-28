OAuth2AuthorizationRequestResolver的主要作用是从提供的Web请求中解析OAuth2AuthorizationRequest。默认实现DefaultOAuth2AuthorizationRequestResolver匹配（默认）路径/ oauth2 / authorization / {registrationId}，提取registrationId并使用它为相关的ClientRegistration构建OAuth2AuthorizationRequest。

OAuth2AuthorizationRequestResolver可以实现的主要用例之一是，可以使用在OAuth 2.0授权框架中定义的标准参数之上的附加参数定制授权请求。

例如，OpenID Connect为[Authorization Code Flow](https://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)定义了额外的OAuth 2.0请求参数，这些参数扩展自OAuth 2.0授权框架[OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749#section-4.1.1)中定义的标准参数。 其中一个扩展参数是prompt参数。

> OPTIONAL。空格分隔，区分大小写的ASCII字符串值列表，指定授权服务器是否提示最终用户进行重新认证和同意。定义的值为：none，login，consent，select\_account

下面的示例展示了如何实现一个OAuth2AuthorizationRequestResolver，它通过包含请求参数prompt=consent来定制oauth2Login\(\)的授权请求。

```
@EnableWebSecurity
public class OAuth2LoginSecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private ClientRegistrationRepository clientRegistrationRepository;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .oauth2Login()
                .authorizationEndpoint()
                    .authorizationRequestResolver(
                            new CustomAuthorizationRequestResolver(
                                    this.clientRegistrationRepository));    1
    }
}

public class CustomAuthorizationRequestResolver implements OAuth2AuthorizationRequestResolver {
    private final OAuth2AuthorizationRequestResolver defaultAuthorizationRequestResolver;

    public CustomAuthorizationRequestResolver(
            ClientRegistrationRepository clientRegistrationRepository) {

        this.defaultAuthorizationRequestResolver =
                new DefaultOAuth2AuthorizationRequestResolver(
                        clientRegistrationRepository, "/oauth2/authorization");
    }

    @Override
    public OAuth2AuthorizationRequest resolve(HttpServletRequest request) {
        OAuth2AuthorizationRequest authorizationRequest =
                this.defaultAuthorizationRequestResolver.resolve(request);  2

        return authorizationRequest != null ?   3
                customAuthorizationRequest(authorizationRequest) :
                null;
    }

    @Override
    public OAuth2AuthorizationRequest resolve(
            HttpServletRequest request, String clientRegistrationId) {

        OAuth2AuthorizationRequest authorizationRequest =
                this.defaultAuthorizationRequestResolver.resolve(
                    request, clientRegistrationId);    4

        return authorizationRequest != null ?   5
                customAuthorizationRequest(authorizationRequest) :
                null;
    }

    private OAuth2AuthorizationRequest customAuthorizationRequest(
            OAuth2AuthorizationRequest authorizationRequest) {

        Map<String, Object> additionalParameters =
                new LinkedHashMap<>(authorizationRequest.getAdditionalParameters());
        additionalParameters.put("prompt", "consent");  6

        return OAuth2AuthorizationRequest.from(authorizationRequest)    7
                .additionalParameters(additionalParameters) 8
                .build();
    }
}
```

1. 配置自定义OAuth2AuthorizationRequestResolver
2. 尝试使用DefaultOAuth2AuthorizationRequestResolver解析OAuth2AuthorizationRequest
3. 如果解析了OAuth2AuthorizationRequest而不是返回自定义版本，则返回null
4. 尝试使用DefaultOAuth2AuthorizationRequestResolver解析OAuth2AuthorizationReques
5. 如果解析了OAuth2AuthorizationRequest而不是返回自定义版本，则返回null
6. 将自定义参数添加到现有OAuth2AuthorizationRequest.additionalParameters
7. 创建默认OAuth2AuthorizationRequest的副本，该副本返回OAuth2AuthorizationRequest.Builder以进行进一步修改
8. 覆盖默认的additionalParameters

> OAuth2AuthorizationRequest.Builder.build（）构造参数OAuth2AuthorizationRequest.authorizationRequestUri，它代表完整的授权请求URI，包括使用application / x-www-form-urlencoded格式的所有查询参数。

上面的示例显示了在标准参数之上添加自定义参数的常见用例。但是，如果您需要删除或更改标准参数或者您的要求更高级，则可以通过简单地覆盖OAuth2AuthorizationRequest.authorizationRequestUri属性来完全控制构建授权请求URI。

以下示例显示了上一示例中customAuthorizationRequest（）方法的变体，而是覆盖了OAuth2AuthorizationRequest.authorizationRequestUri属性。

```
private OAuth2AuthorizationRequest customAuthorizationRequest(
        OAuth2AuthorizationRequest authorizationRequest) {

    String customAuthorizationRequestUri = UriComponentsBuilder
            .fromUriString(authorizationRequest.getAuthorizationRequestUri())
            .queryParam("prompt", "consent")
            .build(true)
            .toUriString();

    return OAuth2AuthorizationRequest.from(authorizationRequest)
            .authorizationRequestUri(customAuthorizationRequestUri)
            .build();
}
```



