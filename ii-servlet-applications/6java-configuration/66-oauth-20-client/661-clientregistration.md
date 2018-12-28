`ClientRegistration`表示在OAuth 2.0或OpenID Connect 1.0 Provider中注册的客户端。

客户端注册保存信息，例如client id, client secret, authorization grant type, redirect URI, scope\(s\), authorization URI, token URI，和其他细节

ClientRegistration 其属性定义如下：

```
public final class ClientRegistration {
    private String registrationId;  1
    private String clientId;    2
    private String clientSecret;    3
    private ClientAuthenticationMethod clientAuthenticationMethod;  4
    private AuthorizationGrantType authorizationGrantType;  5
    private String redirectUriTemplate; 6
    private Set<String> scopes; 7
    private ProviderDetails providerDetails;
    private String clientName;  8

    public class ProviderDetails {
        private String authorizationUri;    9
        private String tokenUri;    10
        private UserInfoEndpoint userInfoEndpoint;
        private String jwkSetUri;   11
        private Map<String, Object> configurationMetadata;  12

        public class UserInfoEndpoint {
            private String uri; 13
            private AuthenticationMethod authenticationMethod;  14
            private String userNameAttributeName;   15

        }
    }
}
```

1. registrationId：唯一标识ClientRegistration的ID。

2. clientId：客户端标识符。

3. clientSecret：客户端密码。

4. clientAuthenticationMethod：用于通过Provider对客户端进行身份验证的方法。 支持的值是**basic**和**post**。

5. authorizationGrantType：OAuth 2.0授权框架定义了四种授权许可[Authorization Grant](https://tools.ietf.org/html/rfc6749#section-1.3)类型。 支持的值是authorization\_code，implicit和client\_credentials。

6. redirectUriTemplate：在最终用户对客户端进行了身份验证和授权访问之后，授权服务器将最终用户的用户代理重定向到客户机的注册重定向URI。

7. scopes：客户端在授权请求流程中请求的范围，例如openid，电子邮件或配置文件。

8. clientName：客户端使用的描述性名称。该名称可用于某些场景，例如在自动生成的登录页面中显示客户端名称时。

9. authorizationUri：授权服务器的授权端点URI。

10. tokenUri：授权服务器的token令牌端点URI。

11. jwkSetUri：用于从授权服务器检索[JSON Web Key \(JWK\)](https://tools.ietf.org/html/rfc7517)集的URI，授权服务器包含用于验证ID令牌的[JSON Web Signature \(JWS\)](https://tools.ietf.org/html/rfc7515)和UserInfo响应\(可选\)的加密密钥。

12. configurationMetadata：OpenID提供程序配置信息。 仅当配置了Spring Boot 2.x属性spring.security.oauth2.client.provider.\[providerId\].issuerUri时，才能使用此信息。

13. \(userInfoEndpoint\)uri:：UserInfo Endpoint URI用于访问经过身份验证的最终用户的声明/属性。

14. \(userInfoEndpoint\)authenticationMethod: 将访问令牌发送到UserInfo端点时使用的身份验证方法。 支持的值是**header**，**form**和**query**。

15. userNameAttributeName：UserInfo Response中返回的属性的名称，该属性引用最终用户的名称或标识符。



