启动Spring Boot 2.x示例并转到http:// localhost:8080。然后，您将被重定向到默认的自动生成的登录页面，该页面显示Google的链接。

点击Google链接，然后您将重定向到Google进行身份验证。

使用您的Google帐户凭据进行身份验证后，显示给您的下一页是“同意”屏幕。“同意”屏幕会要求您允许或拒绝访问您之前创建的OAuth客户端。单击“允许”以授权OAuth客户端访问您的电子邮件地址和基本配置文件信息。

此时，OAuth客户端从UserInfo端点检索您的电子邮件地址和基本配置文件信息，并建立经过身份验证的会话。

