现在您有了一个新的带有谷歌的OAuth客户端，您需要配置应用程序，以便将OAuth客户端用于身份验证流。为此：

1、转到application.yml并设置以下配置：

```
spring:
  security:
    oauth2:
      client:
        registration:   1
          google:   2
            client-id: google-client-id
            client-secret: google-client-secret
```

**Example 6.1. OAuth Client properties**

1. spring.security.oauth2.client.registration是OAuth Client属性的基本属性前缀。

2. 基本属性前缀后面是ClientRegistration的ID，例如google。

2、使用您之前创建的OAuth 2.0凭据替换client-id和client-secret属性中的值。



