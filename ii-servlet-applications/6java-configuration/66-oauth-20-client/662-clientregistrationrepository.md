`ClientRegistrationRepository`用作OAuth 2.0 / OpenID Connect 1.0 `ClientRegistration`的存储库。

> 客户端注册信息最终由关联的授权服务器存储和拥有。此存储库提供检索主客户端注册信息子集的功能，这些信息存储在授权服务器中。

Spring Boot 2.x auto-configuration将spring.security.oauth2.client.registration.\[registrationId\]下的每个属性绑定到ClientRegistration的实例，然后组成ClientRegistrationRepository中的每个ClientRegistration实例。

> ClientRegistrationRepository的默认实现是InMemoryClientRegistrationRepository。

自动配置还将ClientRegistrationRepository注册为ApplicationContext中的@Bean，以便在应用程序需要时可用于依赖注入。

以下清单显示了一个示例：

```
@Controller
public class OAuth2ClientController {

    @Autowired
    private ClientRegistrationRepository clientRegistrationRepository;

    @RequestMapping("/")
    public String index() {
        ClientRegistration googleRegistration =
            this.clientRegistrationRepository.findByRegistrationId("google");

        ...

        return "index";
    }
}
```





