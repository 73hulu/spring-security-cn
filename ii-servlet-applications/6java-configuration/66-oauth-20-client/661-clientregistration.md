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

4. clientAuthenticationMethod：



