`@ RegisteredOAuth2AuthorizedClient`注解提供了将方法参数解析为`OAuth2AuthorizedClient`类型的参数值的功能。与通过OAuth2AuthorizedClientService查找OAuth2AuthorizedClient相比，这是一种方便的替代方法。

```
@Controller
public class OAuth2LoginController {

    @RequestMapping("/userinfo")
    public String userinfo(@RegisteredOAuth2AuthorizedClient("google") OAuth2AuthorizedClient authorizedClient) {
        OAuth2AccessToken accessToken = authorizedClient.getAccessToken();

        ...

        return "userinfo";
    }
}
```

@ RegisteredOAuth2AuthorizedClient注释由OAuth2AuthorizedClientArgumentResolver处理，并提供以下功能：

* 如果客户端尚未获得授权，将自动请求OAuth2AccessToken。
  * 对于authorization\_code，这涉及触发授权请求重定向以启动授权流程
  * 对于client\_credentials，使用DefaultClientCredentialsTokenResponseClient直接从令牌端点获取访问令牌



