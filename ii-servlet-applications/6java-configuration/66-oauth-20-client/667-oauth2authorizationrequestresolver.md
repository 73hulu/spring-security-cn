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





