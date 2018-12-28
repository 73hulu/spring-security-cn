`OAuth2AuthorizedClientRepository`负责在Web请求之间持久化OAuth2AuthorizedClient。然而，`OAuth2AuthorizedClientService`的主要作用是在应用程序级别管理OAuth2AuthorizedClient。

从开发者的角度来看，OAuth2AuthorizedClientRepository或OAuth2AuthorizedClientService提供查找与客户端关联的OAuth2AccessToken的功能，以便可以使用它来启动受保护的资源请求。

> Spring Boot 2.x自动配置OAuth2AuthorizedClientRepository或OAuth2AuthorizedClientService 注册为ApplicationContext中的@Bean。

开发人员还可以在ApplicationContext中注册OAuth2AuthorizedClientRepository或OAuth2AuthorizedClientService @Bean（覆盖Spring Boot 2.x自动配置），以便能够查找与特定ClientRegistration（客户端）关联的OAuth2AccessToken。

以下清单显示了一个示例：

```
@Controller
public class OAuth2LoginController {

    @Autowired
    private OAuth2AuthorizedClientService authorizedClientService;

    @RequestMapping("/userinfo")
    public String userinfo(OAuth2AuthenticationToken authentication) {
        // authentication.getAuthorizedClientRegistrationId() returns the
        // registrationId of the Client that was authorized during the oauth2Login() flow
        OAuth2AuthorizedClient authorizedClient =
            this.authorizedClientService.loadAuthorizedClient(
                authentication.getAuthorizedClientRegistrationId(),
                authentication.getName());

        OAuth2AccessToken accessToken = authorizedClient.getAccessToken();

        ...

        return "userinfo";
    }
}
```





